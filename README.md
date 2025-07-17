# C Language Format Configuration

A carefully crafted clang-format configuration optimized for C development, emphasizing readability and consistency.

## Features

- **Function Declaration Style**: Return type and function name stay on the same line
- **Parameter Alignment**: Clean parameter alignment with proper indentation
- **Balanced Line Length**: Moderate tolerance for exceeding column limits to avoid excessive line breaks
- **Embedded C Friendly**: Optimized for embedded systems and low-level C code
- **Consistent Formatting**: Unified style across function declarations, calls, and definitions

## Configuration Highlights

| Setting | Value | Purpose |
|---------|-------|---------|
| `ColumnLimit` | 100 | Reasonable line length for modern displays |
| `PenaltyReturnTypeOnItsOwnLine` | 1000 | Strongly prefer return type on same line as function name |
| `PenaltyBreakBeforeFirstCallParameter` | 100 | Moderate preference for keeping first parameter on same line |
| `PenaltyExcessCharacter` | 10 | Allow modest line length overruns |
| `AlignAfterOpenBracket` | Align | Clean parameter alignment |
| `BinPackParameters` | false | One parameter per line when wrapping |

## Usage

### Method 1: Direct Usage (Recommended)
```bash
# Format specific files
clang-format -style=file:myC.clang-format -i *.c *.h

# Format entire directory recursively
find . -name "*.c" -o -name "*.h" | xargs clang-format -style=file:myC.clang-format -i
```

### Method 2: Copy as Default Configuration
```bash
# Copy to your project root
cp myC.clang-format .clang-format

# Then use standard clang-format commands
clang-format -i *.c *.h
```

### Method 3: Integration with Build Systems

**Makefile:**
```makefile
CLANG_FORMAT_STYLE = file:path/to/myC.clang-format
SOURCES = $(wildcard *.c *.h)

format:
	clang-format -style=$(CLANG_FORMAT_STYLE) -i $(SOURCES)

format-check:
	clang-format -style=$(CLANG_FORMAT_STYLE) --dry-run --Werror $(SOURCES)
```

**CMake:**
```cmake
find_program(CLANG_FORMAT_EXECUTABLE clang-format)
if(CLANG_FORMAT_EXECUTABLE)
    file(GLOB_RECURSE ALL_SOURCE_FILES *.c *.h)
    add_custom_target(format
        COMMAND ${CLANG_FORMAT_EXECUTABLE} -style=file:${CMAKE_SOURCE_DIR}/myC.clang-format -i ${ALL_SOURCE_FILES}
        WORKING_DIRECTORY ${CMAKE_SOURCE_DIR}
    )
endif()
```

## Formatting Examples

### Function Declarations
```c
// Before formatting
static inline void
nrz_dev_init(uint32_t strip_i, FLEXIO_Type* base, uint8_t chn_pin, uint8_t sender_type);

// After formatting
static inline void nrz_dev_init(uint32_t strip_i, 
                                FLEXIO_Type* base,
                                uint8_t chn_pin,
                                uint8_t sender_type);
```

### Function Calls
```c
// Before formatting
result = calculate_checksum(data_buffer,buffer_length,initial_seed,flags);

// After formatting
result = calculate_checksum(data_buffer, buffer_length, 
                           initial_seed, flags);
```

### Struct Definitions
```c
// Consistent alignment and spacing
typedef struct {
    uint32_t    device_id;
    uint8_t     channel_mask;
    bool        is_enabled;
    const char* device_name;
} device_config_t;
```

## Editor Integration

### Visual Studio Code
Add to your workspace settings:
```json
{
    "C_Cpp.clang_format_style": "file:path/to/myC.clang-format",
    "editor.formatOnSave": true
}
```

### Vim/Neovim
```vim
" Add to your .vimrc
let g:clang_format#style_options = {
    \ "style": "file:path/to/myC.clang-format"
    \ }
```

### CLion/IntelliJ
1. Go to Settings → Editor → Code Style → C/C++
2. Choose "Set from..." → Predefined Style → Custom
3. Import your `myC.clang-format` file

## Requirements

- **clang-format** version 10.0 or later
- Compatible with C89, C99, C11, and C17 standards

## Customization

Feel free to adjust the configuration to match your project's needs:

1. **Modify line length**: Change `ColumnLimit` value
2. **Adjust penalties**: Fine-tune penalty values for different formatting choices
3. **Indentation**: Modify `IndentWidth` and related settings
4. **Brace style**: Update `BreakBeforeBraces` if needed

## Contributing

If you find improvements or have suggestions for better C formatting rules, feel free to:
1. Open an issue with examples
2. Submit a pull request with your changes
3. Share your use case and formatting preferences

## License

This configuration is released under the MIT License. Feel free to use, modify, and distribute as needed.

---

*Last updated: [Current Date]*
*Tested with: clang-format 14.0+*
