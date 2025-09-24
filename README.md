Bihar AgMCP - Claude Desktop Integration Guide
Overview

Bihar AgMCP (Agricultural Model Control Protocol) is a specialized MCP server that integrates with Claude Desktop to provide AI-powered agricultural weather alerts for Bihar, India. This integration allows Claude to access real-time weather data, crop information, and generate personalized farming recommendations directly within the Claude Desktop interface.

What is MCP (Model Control Protocol)?

MCP is a protocol that allows AI assistants like Claude to connect to external tools and data sources. In this case, the Bihar AgMCP server acts as a bridge between Claude and agricultural data systems, enabling Claude to:

Generate location-specific weather alerts

Provide crop-specific recommendations

Access Bihar district and village data

Create multi-channel communication messages (SMS, WhatsApp, etc.)

Installation & Setup
Prerequisites

Claude Desktop application installed

Python 3.8+ installed on your system

Required Python packages (see requirements.txt)

Step 1: Install Dependencies
pip install -r requirements.txt

Step 2: Configure Claude Desktop

Add the Bihar AgMCP server to your Claude Desktop configuration file:

Location of config file:

macOS: ~/Library/Application Support/Claude/claude_desktop_config.json

Windows: %APPDATA%\Claude\claude_desktop_config.json

Configuration:

{
  "mcpServers": {
    "bihar-agmcp": {
      "command": "python",
      "args": ["/path/to/your/bihar_agmcp_server.py"],
      "env": {
        "OPENAI_API_KEY": "your-openai-api-key-here"
      }
    }
  }
}

Step 3: Environment Variables (Optional)

Create a .env file in your project directory for additional configuration:

OPENAI_API_KEY=your-openai-api-key-here
LOG_LEVEL=INFO

Step 4: Restart Claude Desktop

After adding the configuration, restart Claude Desktop to load the MCP server.

Available Tools in Claude

Once integrated, Claude Desktop will have access to these Bihar AgMCP tools:

1. generate_weather_alert

Purpose: Generate comprehensive weather alerts for Bihar districts

Parameters:

district (required): Bihar district name (e.g., "Patna", "Gaya", "Muzaffarpur")

include_ai_analysis (optional): Whether to include AI-powered analysis (default: true)

Example Usage in Claude:

Generate a weather alert for Patna district

2. get_district_crops

Purpose: Get crop information for specific Bihar districts

Parameters:

district (required): Bihar district name

Example Usage in Claude:

What are the primary crops grown in Muzaffarpur district?

3. get_crop_calendar

Purpose: Get detailed crop calendar information

Parameters:

crop (required): Crop name (rice, wheat, maize, sugarcane, mustard)

Example Usage in Claude:

Show me the rice crop calendar with planting and harvesting schedules

4. get_weather_data

Purpose: Get weather data for specific coordinates

Parameters:

latitude (required): Latitude coordinate

longitude (required): Longitude coordinate

days (optional): Number of forecast days (1-7, default: 3)

Example Usage in Claude:

Get weather data for coordinates 25.5941, 85.1376 for the next 5 days

5. generate_agent_messages

Purpose: Generate messages for different communication channels

Parameters:

alert_data (required): Alert data object

channels (optional): Array of channels "sms","whatsapp","ussd","ivr","telegram"

Example Usage in Claude:

Generate SMS and WhatsApp messages for the latest weather alert

6. list_bihar_districts

Purpose: Get list of all supported Bihar districts

Example Usage in Claude:

Show me all Bihar districts supported by the system

7. help_bihar_agmcp

Purpose: Get comprehensive help and usage examples

Parameters:

topic (optional): Specific help topic ("overview", "districts", "crops", "weather", "alerts", "examples")

Example Usage in Claude:

Help me understand how to use the Bihar AgMCP system

Usage Examples in Claude Desktop
Basic Weather Alert Generation

User: "Generate a weather alert for Patna district"

Claude Response: Claude will use the generate_weather_alert tool to provide:

Current weather conditions

Crop-specific recommendations

Seasonal agricultural advice

Action items for farmers

AI-powered insights (if OpenAI API key is configured)

Crop Planning Assistance

User: "I'm a farmer in Darbhanga. What crops should I plant this season?"

Claude Response: Claude will:

Use get_district_crops to get Darbhanga-specific crop information

Consider current season (Kharif/Rabi/Zaid)

Provide planting recommendations

Show crop calendar information

Multi-Channel Communication

User: "Create SMS and WhatsApp messages for farmers about the latest weather alert in Gaya"

Claude Response: Claude will:

Generate a weather alert for Gaya

Use generate_agent_messages to create formatted messages

Provide SMS-optimized short messages

Create rich WhatsApp messages with emojis and formatting

Features & Capabilities
🌾 Agricultural Intelligence

Crop-Specific Alerts: Tailored recommendations based on crop type and growth stage

Seasonal Awareness: Considers Kharif, Rabi, and Zaid seasons

District Specialization: Knows primary, secondary, and specialty crops for each Bihar district

🌤️ Weather Integration

Real-time Data: Integrates with weather APIs (Open-Meteo, Tomorrow.io, etc.)

Forecast Analysis: Multi-day weather predictions

Alert Generation: Automated alerts based on weather conditions

🤖 AI Enhancement

OpenAI Integration: Enhanced insights when API key is provided

Contextual Recommendations: AI-powered farming advice

Natural Language: Human-friendly alert messages

📱 Multi-Channel Support

SMS: Short, concise alerts for basic phones

WhatsApp: Rich formatted messages with emojis

USSD: Interactive menu-based alerts

IVR: Voice-based alert scripts

Telegram: Bot-friendly formatted messages

Supported Bihar Districts

The system supports all 38 districts of Bihar:

Major Districts: Patna, Gaya, Bhagalpur, Muzaffarpur, Darbhanga, Siwan, Begusarai, Katihar

Complete List: Use the list_bihar_districts tool in Claude to see all supported districts.

Crop Calendar Support

Supported Crops:

Rice (Kharif season)

Wheat (Rabi season)

Maize (Kharif/Zaid seasons)

Sugarcane (Annual crop)

Mustard (Rabi season)

Each crop includes:

Planting and harvesting periods

Growth stages

Duration estimates

Seasonal recommendations

Troubleshooting
Common Issues

1. MCP Server Not Loading

Check Claude Desktop configuration file syntax

Verify Python path and script location

Restart Claude Desktop after configuration changes

2. Tool Execution Errors

Check Python dependencies are installed

Verify environment variables (if using .env file)

Check logs for specific error messages

3. Limited AI Features

Ensure OPENAI_API_KEY is set in configuration

Verify API key has sufficient credits

Check network connectivity

Debug Mode

Enable debug logging by setting LOG_LEVEL=DEBUG in your environment variables.

Verification

Test the integration by asking Claude:

List all available Bihar AgMCP tools


Claude should respond with the complete list of 7 tools if the integration is working correctly.

Advanced Configuration
Custom Weather APIs

The system supports multiple weather data sources. Configure additional APIs in your environment:

TOMORROW_IO_API_KEY=your-tomorrow-io-key
OPENWEATHERMAP_API_KEY=your-openweather-key
ACCUWEATHER_API_KEY=your-accuweather-key

Logging Configuration

Adjust logging levels for debugging:

{
  "mcpServers": {
    "bihar-agmcp": {
      "command": "python",
      "args": ["/path/to/bihar_agmcp_server.py"],
      "env": {
        "LOG_LEVEL": "DEBUG"
      }
    }
  }
}

Security Considerations

API Keys: Store sensitive API keys in environment variables, not in code

File Permissions: Ensure the MCP server script has appropriate permissions

Network Access: The server requires internet access for weather data APIs

Support & Development
Getting Help

Use the help_bihar_agmcp tool within Claude

Check the server logs for error messages

Verify your Claude Desktop configuration

Contributing

The Bihar AgMCP system is designed to be extensible. You can:

Add new weather data sources

Extend crop calendar information

Add support for additional districts

Enhance AI analysis capabilities

Version Information

MCP Protocol: Compatible with Claude Desktop MCP implementation

Python Version: Requires Python 3.8+

Dependencies: See requirements.txt for complete list

This integration brings the power of agricultural intelligence directly into Claude Desktop, enabling farmers, agricultural extension workers, and researchers to access localized weather and crop information through natural language conversations.