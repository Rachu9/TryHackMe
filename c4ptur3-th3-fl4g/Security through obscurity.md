# Security Through Obscurity

Security through obscurity is the reliance in security engineering on the secrecy of the design or implementation as the main method of providing security for a system or component of a system.

## Command Breakdown

The command sequence you provided is used in a Unix-like environment (like Linux or macOS) to navigate to a directory and extract readable text from a binary file, such as an image. Here’s a breakdown of each command:

### Command Sequence

1. **`cd Desktop`**
   - **Explanation**: This command changes the current working directory to the Desktop directory.
   - **Usage**: `cd` stands for "change directory." If you were in a different directory (like your home directory or another folder), executing this command would move you to the Desktop folder, allowing you to access files located there.

2. **`strings meme_1559010886025.jpg`**
   - **Explanation**: This command uses the `strings` utility to extract and display printable strings from the specified binary file (`meme_1559010886025.jpg`).
   - **Usage**:
     - **`strings`**: This is a command-line utility that scans files for sequences of printable characters (ASCII or Unicode) and outputs them. It's commonly used to find human-readable text in binary files, such as images or executable files.
     - **`meme_1559010886025.jpg`**: This is the name of the file you are analyzing. It's likely an image file that may contain embedded text, comments, or other readable information.

## Summary of the Entire Process
1. Navigate to the Desktop directory to access your desired file.
2. Use the `strings` command to find and display any readable text found within the `meme_1559010886025.jpg` image file.

## Why Use `strings`?
The `strings` command is particularly useful in various scenarios, including:
- **Digital Forensics**: Investigators may look for hidden messages or metadata in image files.
- **Software Analysis**: Developers might want to examine binary files for hardcoded strings, version information, or debugging messages.
- **Malware Analysis**: Security researchers can analyze executable files to find text that could provide insights into the behavior or purpose of the code.

In this specific case, running `strings meme_1559010886025.jpg` may reveal any captions, comments, or metadata associated with the meme image that could give more context or information about its content.
### Answer

> **Download and get 'inside' the file. What is the first filename & extension?.**  
> _hackerchat.png_

> **Get inside the archive and inspect the file carefully. Find the hidden text.**  
> _AHH_YOU_FOUND_ME!_

