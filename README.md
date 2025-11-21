# Caesar Cipher (GUI + CLI)

A simple, user-friendly Caesar cipher tool that can encrypt and decrypt text. It provides a polished desktop GUI built with Tkinter and a non-interactive CLI for quick terminal usage.

## Features
- Encrypt and decrypt any text using a shift value
- Preserves letter case; non-letter characters stay unchanged
- GUI with shift control, Encrypt/Decrypt toggle, output area
- Copy output to clipboard and Save output to a file
- CLI mode for scripting and quick use

## Requirements
- Python 3.8+

## Installation
Clone or download the repository and make sure you can run Python:

```bash
# On Windows (recommended)
py --version

# On macOS/Linux
python3 --version
```

## Run the GUI
```bash
# Windows
py caesar_cipher.py

# macOS/Linux
python3 caesar_cipher.py
```

## CLI Usage
Process text directly from the terminal without opening the GUI.

```bash
# Encrypt
py caesar_cipher.py --text "Hello, World!" --shift 3 --mode encrypt

# Decrypt
py caesar_cipher.py --text "Khoor, Zruog!" --shift 3 --mode decrypt
```

Options:
- `--text` The input message to process
- `--shift` Integer shift value (can be negative); default `3`
- `--mode` Either `encrypt` or `decrypt`; default `encrypt`
- `--cli` Force CLI mode even without `--text`

## How It Works
- Letters A–Z and a–z are rotated using modular arithmetic.
- Uppercase and lowercase letters are handled separately; punctuation and spaces remain unchanged.

Core implementation lives in `caesar_cipher.py`:
- Character rotation: `caesar_cipher.py:6`
- String transform: `caesar_cipher.py:12`
- Encryption wrapper: `caesar_cipher.py:16`
- Decryption wrapper: `caesar_cipher.py:19`
- GUI app: `caesar_cipher.py:29`
- CLI parsing: `caesar_cipher.py:132`

## Tips
- On Windows, prefer the `py` launcher; `python` may be an alias that is disabled.
- Negative shifts work (e.g., `--shift -5`), and large shifts are reduced modulo 26.

## License
MIT
