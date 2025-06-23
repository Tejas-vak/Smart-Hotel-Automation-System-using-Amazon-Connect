# Voicemail Integration for Amazon Connect

This folder contains the complete setup for enabling voicemail functionality in an Amazon Connect contact center using AWS Lambda and contact flows.

## 📁 Contents

- **kvsrealtimeTranscriber**: Lambda function responsible for initiating real-time transcription from Kinesis Video Streams. It also triggers the consumer function using environment variables.
- **kvsrealtimeConsumer**: Lambda function that processes the transcription data and handles downstream logic such as storing or analyzing the voicemail content.
- **Environment Variable Screenshots**: Visual references showing the configuration of environment variables for both Lambda functions.
- **IdeathonVM Contact Flow**: A pre-built Amazon Connect contact flow designed to handle voicemail interactions. This flow is integrated into the Main Contact Flow to support voicemail capture and processing.

## 🔁 Integration Details

The `kvsrealtimeConsumer` function is invoked from within the `kvsrealtimeTranscriber` function using environment variables. This allows for modular and dynamic invocation without hardcoding function names.

The `IdeathonVM` flow is designed to be imported into Amazon Connect and linked from the Main Contact Flow wherever voicemail functionality is required.

## ⚙️ Optional Usage

If you find the setup of the `IdeathonVM` flow and Lambda functions too complex or unnecessary for your use case, you can modify the contact flows to omit the voicemail functionality entirely.

This setup is intended to provide a robust and extensible voicemail solution, but it is fully optional and customizable based on your project needs.
