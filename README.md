# ygoimgen.sh  
A bash-based Yu-Gi-Oh! card image generator that converts card data (from a SQLite database) and custom artwork into official-style card images. Uses `sqlite3` for data handling and `imagemagick` for image rendering.  


## Features  
- **Official-Style Output**: Generates cards matching the classic Yu-Gi-Oh! template (artwork, name, type, ATK/DEF, effect text, etc.).  
- **Customizable**: Use your own artwork and card data.  
- **Lightweight**: No heavy dependencies—just bash, `sqlite3`, and `imagemagick`.  


## Prerequisites  
Install required tools before running:  

### Debian/Ubuntu  
```bash
sudo apt update && sudo apt install sqlite3 imagemagick
```

### macOS (Homebrew)  
```bash
brew install sqlite imagemagick
```

### Windows  
- Use [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) (Windows Subsystem for Linux) or a bash-compatible terminal (e.g., Git Bash).  
- Install dependencies via WSL’s package manager (e.g., `sudo apt install sqlite3 imagemagick`).  


## Setup  

### 1. Clone the Repository  
```bash
git clone https://github.com/ZisIsNotZis/ygoimgen.sh.git
cd ygoimgen.sh
```

### 2. Prepare Card Data (SQLite Database)  
The generator uses `cards.cdb` (a SQLite database) to store card details. An empty `cards.cdb` is provided—you’ll need to populate it with your card data.  

#### How to Populate the Database  
Use `sqlite3` to insert data into `cards.cdb`

### 3. Add Custom Artwork  
Place your card artwork in the `pico/` directory. The file name **must match the card’s `id`** (from `cards.cdb`) and use a common image format (PNG, JPG, etc.).  

Example:  
- For card `id=12345678`, save artwork as `pico/12345678.png`.  
- For card `id=87654321`, save artwork as `pico/87654321.jpg`.  


## Usage  
Run the generator script to create card images:  
```bash
./gen.sh
```

### What It Does  
1. Reads all card data from `cards.cdb`.  
2. For each card:  
   - Loads artwork from `pico/<id>.<ext>`.  
   - Renders the card using `imagemagick` (applies template, text, ATK/DEF, etc.).  
3. Saves the final card image to `pic/<id>.jpg`.  


## Example Output  
After running `./gen.sh`, you’ll find:  
- `pic/12345678.jpg` (Dark Magician card with your artwork).  
- `pic/87654321.jpg` (Mystical Space Typhoon spell card).  


## Customization  
Tweak the script or template to match your preferences:  

### 1. Modify the Card Template  
The script uses an internal template (colors, fonts, layout). Edit `gen.sh` to adjust:  
- Fonts (replace `Arial` with your preferred font).  
- Colors (change hex codes for borders, text, or backgrounds).  
- Layout (adjust text positions, artwork size, etc.).  

### 2. Add More Card Fields  
If your `cards.cdb` has extra fields (e.g., `race` for monsters), update the script to include them in the output.  


## Troubleshooting  

### 1. "sqlite3: command not found" or "convert: command not found"  
- Ensure `sqlite3` and `imagemagick` are installed (see [Prerequisites](#prerequisites)).  

### 2. Artwork Not Loading  
- Verify the artwork file name matches the card’s `id` (e.g., `pico/12345678.png` for `id=12345678`).  
- Check that the image format is supported (PNG, JPG, GIF, etc.).  

### 3. Text Overlaps or Cut Off  
- Shorten long effect text (use `\n` to add line breaks in the `effect` column).  
- Adjust font sizes in `gen.sh` (look for `font-size` parameters in `convert` commands).  


## License  
This project is licensed under the **MIT License**—see the [LICENSE](LICENSE) file for details.  


## Contributing  
Contributions are welcome! To improve the script:  
1. Fork the repository.  
2. Create a feature branch (`git checkout -b feature/your-feature`).  
3. Commit changes (`git commit -m "Add X feature"`).  
4. Push to the branch (`git push origin feature/your-feature`).  
5. Open a Pull Request.  

Ideas for improvement:  
- Add support for more card types (Xyz, Synchro, Pendulum).  
- Include a default template for missing artwork.  
- Add batch processing for large databases.  