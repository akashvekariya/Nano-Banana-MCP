# Nano-Banana MCP Server 🍌

> **🤖 This project was forked from [ConechoAI/Nano-Banana-MCP](https://github.com/ConechoAI/Nano-Banana-MCP)** and enhanced with configurable model support.

A Model Context Protocol (MCP) server that provides AI image generation and editing capabilities using Google's Gemini Image API. Generate stunning images, edit existing ones, and iterate on your creations with simple text prompts.

**Now supports both Gemini 3 Pro Image (Nano Banana Pro) and Gemini 2.5 Flash Image!**

## ✨ Features

- 🎨 **Generate Images**: Create new images from text descriptions
- ✏️ **Edit Images**: Modify existing images with text prompts
- 🔄 **Iterative Editing**: Continue editing the last generated/edited image
- 🖼️ **Multiple Reference Images**: Use reference images for style transfer and guidance
- 🌍 **Cross-Platform**: Smart file paths for Windows, macOS, and Linux
- 🔧 **Easy Setup**: Simple configuration with API key
- 📁 **Auto File Management**: Automatic image saving with organized naming
- 🔀 **Configurable Models**: Switch between Gemini 3 Pro Image and Gemini 2.5 Flash Image

## 🤖 Available Models

| Model | Slug | Description |
|-------|------|-------------|
| **Gemini 3 Pro Image** | `gemini-3-pro-image-preview` | Highest quality, advanced reasoning (Default) |
| **Gemini 2.5 Flash Image** | `gemini-2.5-flash-image` | Fast, high-volume generation |

## 🔑 Setup

1. **Get your Gemini API key**:
   - Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
   - Create a new API key
   - Copy it for configuration

2. **Configure the MCP server**:
   See configuration examples for your specific client below (Claude Code, Cursor, or other MCP clients).

## 💻 Usage with Claude Code

### Configuration:

Add this to your Claude Code MCP settings:

**Option A: With environment variable (Recommended - Most Secure)**
```json
{
  "mcpServers": {
    "nano-banana": {
      "command": "npx",
      "args": ["@akashvekariya/nano-banana-mcp"],
      "env": {
        "GEMINI_API_KEY": "your-gemini-api-key-here",
        "GEMINI_MODEL": "gemini-3-pro-image-preview"
      }
    }
  }
}
```

**Option B: Install from GitHub directly**
```json
{
  "mcpServers": {
    "nano-banana": {
      "command": "npx",
      "args": ["-y", "github:akashvekariya/Nano-Banana-MCP"],
      "env": {
        "GEMINI_API_KEY": "your-gemini-api-key-here",
        "GEMINI_MODEL": "gemini-3-pro-image-preview"
      }
    }
  }
}
```

**Option C: Without environment variable**
```json
{
  "mcpServers": {
    "nano-banana": {
      "command": "npx",
      "args": ["@akashvekariya/nano-banana-mcp"]
    }
  }
}
```

### Usage Examples:
```
Generate an image of a sunset over mountains
```

```
Edit this image to add some birds in the sky
```

```
Continue editing to make it more dramatic
```

## 🎯 Usage with Cursor

### Configuration:

Add to your Cursor MCP configuration:

**Option A: With environment variable (Recommended)**
```json
{
  "nano-banana": {
    "command": "npx",
    "args": ["@akashvekariya/nano-banana-mcp"],
    "env": {
      "GEMINI_API_KEY": "your-gemini-api-key-here",
      "GEMINI_MODEL": "gemini-3-pro-image-preview"
    }
  }
}
```

**Option B: Without environment variable**
```json
{
  "nano-banana": {
    "command": "npx",
    "args": ["@akashvekariya/nano-banana-mcp"]
  }
}
```

### Usage Examples:
- Ask Cursor to generate images for your app
- Create mockups and prototypes
- Generate assets for your projects

## 🔧 For Other MCP Clients

If you're using a different MCP client, you can configure nano-banana-mcp using any of these methods:

### Configuration Methods

**Method A: Environment Variable in MCP Config (Recommended)**
```json
{
  "nano-banana": {
    "command": "npx",
    "args": ["@akashvekariya/nano-banana-mcp"],
    "env": {
      "GEMINI_API_KEY": "your-gemini-api-key-here",
      "GEMINI_MODEL": "gemini-3-pro-image-preview"
    }
  }
}
```

**Method B: System Environment Variable**
```bash
export GEMINI_API_KEY="your-gemini-api-key-here"
export GEMINI_MODEL="gemini-3-pro-image-preview"
npx @akashvekariya/nano-banana-mcp
```

**Method C: Using the Configure Tool**
```bash
npx @akashvekariya/nano-banana-mcp
# The server will prompt you to configure when first used
# This creates a local .nano-banana-config.json file
```

## 🌐 Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `GEMINI_API_KEY` | Yes | - | Your Gemini API key from Google AI Studio |
| `GEMINI_MODEL` | No | `gemini-3-pro-image-preview` | Model to use for image generation |

## 🛠️ Available Commands

### `generate_image`
Create a new image from a text prompt.
```typescript
generate_image({
  prompt: "A futuristic city at night with neon lights",
  aspectRatio: "16:9",    // optional
  resolution: "2K",       // optional
  useGoogleSearch: true   // optional
})
```

### `edit_image`
Edit a specific image file.
```typescript
edit_image({
  imagePath: "/path/to/image.png",
  prompt: "Add a rainbow in the sky",
  referenceImages: ["/path/to/reference.jpg"], // optional
  aspectRatio: "16:9",    // optional
  resolution: "2K",       // optional
  useGoogleSearch: false  // optional
})
```

### `continue_editing`
Continue editing the last generated/edited image.
```typescript
continue_editing({
  prompt: "Make it more colorful",
  referenceImages: ["/path/to/style.jpg"], // optional
  aspectRatio: "9:16",    // optional
  resolution: "4K",       // optional
  useGoogleSearch: false  // optional
})
```

### 📐 Aspect Ratio Options

| Value | Use Case |
|-------|----------|
| `1:1` | Square (default), Instagram post |
| `16:9` | Widescreen, landscape, desktop, YouTube thumbnail |
| `9:16` | Portrait, mobile, vertical, TikTok, Instagram Reels/Stories |
| `4:3` | Standard landscape |
| `3:4` | Standard portrait |
| `4:5` | Instagram portrait |
| `5:4` | Instagram landscape |
| `3:2` | Classic photo landscape |
| `2:3` | Classic photo portrait |
| `21:9` | Ultrawide, cinematic |

### 🖼️ Resolution Options

| Value | Size | Use Case |
|-------|------|----------|
| `1K` | 1024px | Fast generation (default) |
| `2K` | 2048px | High quality |
| `4K` | 4096px | Ultra quality, print (Gemini 3 Pro only) |

### `get_available_models`
List all available Gemini image generation models and show which one is currently active.
```typescript
get_available_models()
```

### `set_model`
Switch to a different model during the session. Use this when you want faster generation or higher quality.
```typescript
set_model({
  model: "gemini-2.5-flash-image" // or "gemini-3-pro-image-preview"
})
```

### `get_last_image_info`
Get information about the last generated image.
```typescript
get_last_image_info()
```

### `configure_gemini_token`
Configure your Gemini API key.
```typescript
configure_gemini_token({
  apiKey: "your-gemini-api-key"
})
```

### `get_configuration_status`
Check if the API key is configured and which model is active.
```typescript
get_configuration_status()
```

## ⚙️ Configuration Priority

The MCP server loads your configuration in the following priority order:

1. **🥇 MCP Configuration Environment Variables** (Highest Priority)
   - Set in your `claude_desktop_config.json` or MCP client config
   - Most secure as it's contained within the MCP configuration
   - Example: `"env": { "GEMINI_API_KEY": "your-key", "GEMINI_MODEL": "gemini-3-pro-image-preview" }`

2. **🥈 System Environment Variables**
   - Set in your shell/system environment
   - Example: `export GEMINI_API_KEY="your-key"`

3. **🥉 Local Configuration File** (Lowest Priority)
   - Created when using the `configure_gemini_token` tool
   - Stored as `.nano-banana-config.json` in current directory
   - Automatically ignored by Git and NPM

**💡 Recommendation**: Use Method 1 (MCP config env variables) for the best security and convenience.

## 📁 File Storage

Images are automatically saved to platform-appropriate locations:

- **Windows**: `%USERPROFILE%\\Documents\\nano-banana-images\\`
- **macOS/Linux**: `./generated_imgs/` (in current directory)
- **System directories**: `~/nano-banana-images/` (when run from system paths)

File naming convention:
- Generated images: `generated-[timestamp]-[id].png`
- Edited images: `edited-[timestamp]-[id].png`

## 🎨 Example Workflows

### Basic Image Generation
1. `generate_image` - Create your base image
2. `continue_editing` - Refine and improve
3. `continue_editing` - Add final touches

### Style Transfer
1. `generate_image` - Create base content
2. `edit_image` - Use reference images for style
3. `continue_editing` - Fine-tune the result

### Iterative Design
1. `generate_image` - Start with a concept
2. `get_last_image_info` - Check current state
3. `continue_editing` - Make adjustments
4. Repeat until satisfied

## 🔧 Development

This project uses the following technologies:

- **TypeScript** - Type-safe development
- **Node.js** - Runtime environment
- **Zod** - Schema validation
- **Google GenAI** - Image generation API
- **MCP SDK** - Model Context Protocol

### Local Development

```bash
# Clone the repository
git clone https://github.com/akashvekariya/Nano-Banana-MCP.git
cd Nano-Banana-MCP

# Install dependencies
npm install

# Run in development mode
npm run dev

# Build for production
npm run build

# Run tests
npm test
```

## 📋 Requirements

- Node.js 18.0.0 or higher
- Gemini API key from Google AI Studio
- Compatible with Claude Code, Cursor, and other MCP clients

## 🤝 Contributing

Contributions are welcome! Please feel free to:

- Report bugs
- Suggest new features
- Submit pull requests
- Improve documentation

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **[ConechoAI/Nano-Banana-MCP](https://github.com/ConechoAI/Nano-Banana-MCP)** - Original project
- **[Claude Code](https://claude.ai/code)** - For generating the original project
- **Google AI** - For the powerful Gemini Image API
- **Anthropic** - For the Model Context Protocol
- **Open Source Community** - For the amazing tools and libraries

## 📞 Support

- 🐛 **Issues**: [GitHub Issues](https://github.com/akashvekariya/Nano-Banana-MCP/issues)
- 📖 **Documentation**: This README and inline code comments
- 💬 **Discussions**: [GitHub Discussions](https://github.com/akashvekariya/Nano-Banana-MCP/discussions)

---

*✨ Fork of the original [Nano-Banana-MCP](https://github.com/ConechoAI/Nano-Banana-MCP) with configurable model support!*
