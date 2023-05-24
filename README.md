# DocsInARow: A Document and Image Categorization Tool

<img src="logo.png" alt="Logo" width="200" height="200" style="float: right;">

DocsInARow is a Python application for scanning and analyzing images or documents. The tool is designed to read and interpret the text contained in scanned documents and categorize the document type using the GPT-3 model provided by OpenAI. For images, it uses Google Vision to detect labels and categories.

## Features

1. Text extraction from images using Optical Character Recognition (OCR) with Tesseract.
2. Text correction and formatting using OpenAI's GPT-3 model.
3. Document categorization using GPT-3.
4. Label detection in images using Google Vision.
5. Image metadata editing to include corrected text.

## Setup

1. Clone the repository or download the Python script.

2. Install necessary dependencies with pip:

   ```bash
   pip install pytesseract openai google-cloud-vision piexif
    ```

3. Set up Tesseract-OCR on your system and update the path in the script:

    ```python
    pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
    ```

4. Replace the OpenAI API key and Google Cloud Vision API key with your own in the script:

    ```python
    openai.api_key = 'your-openai-api-key'
    os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "your-google-cloud-vision-key.json"
    ```
5. Place your images in the Pictures directory or change the pictures_dir variable to your preferred directory:

    ```python
    pictures_dir = "E:\\Pictures"
    ```

6. Run the script:

    ```bash
    python main.py
    ```

## Supported File Formats

DocsInARow supports the following file formats:

- Images: JPG
- Documents: JPG

Currently, during development it only supports JPG files. This is because this project orginally started out as a way to organize my scanned documents that I got in the mail. In the future we will expand this to include a large variety of file types.

## Usage

Run the Python script. The script will go through each image in the directory.

For each image:

If the image contains more than 25 words, it is considered a document. The script extracts the text, corrects it using GPT-3, and prints out the corrected text. It also categorizes the document using GPT-3 and adds the corrected text to the image's metadata.
If the image contains less than 25 words, it is considered a picture. The script uses Google Vision to detect labels and prints them out.
After each image, the script asks whether you want to continue to the next image. You can type 'Y' to continue or 'N' to stop the script.

## Notes

The tool uses the OpenAI text-davinci-003 model, which has a maximum context length of 4096 tokens. This limit includes both the prompt text and the completion, so ensure your text to correct and categorize fits within this limit.

Please also be aware of the usage costs associated with the OpenAI API and Google Cloud Vision API.

## Project Structure

The DocsInARow project follows a specific structure to organize its code and resources. Here's an overview of the project structure:

```
DocsInARow/   
├── tests/
│   └── test_text_processing.py
|   └── test_image.jpg
├── config.py
├── image_processing.py
├── main.py
├── text_processing.py
├── .env
└── README.md
```

## Brief Explanation of Each Python File

* `config.py`: Handles loading and setting configuration parameters for the application. It loads configuration from the config.json file and sets environment variables required by other modules.

* `image_processing.py`: Contains functions for image-related processing tasks. It retrieves image files from a specified directory, adds text to image metadata, and moves files to date-specific directories for organizing the processed images.

* `main.py`: Serves as the main entry point of the application. It orchestrates the overall image processing workflow, calling functions from other modules to extract and correct text from images.

* `text_processing.py`: Provides functions for text-related processing tasks. It includes functions to extract text from images using OCR, correct text using OpenAI's GPT-3 model, categorize documents using GPT-3, and generate meaningful filenames.

* `tests/test_text_processing.py`: Contains unit tests for the functions in `text_processing.py`. It ensures that the text processing functions are working as expected.

## Contribution

Contributions are welcome! Please feel free to submit a Pull Request or open an Issue.

## License

DocsInARow is open-source software licensed under the MIT license.