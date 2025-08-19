# Manga Downloader Guide Using Google Colab - By Ronak 📚

[![Open in Google Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

*Download manga chapters directly in your browser as high-quality PDFs - No installations required!*

---

## ✨ Features
- 🌐 **Web-Based** - No software installs needed
- 🖼️ **HD Quality** - Preserves original image resolution
- 🔒 **Virus-Free** - 100% secure cloud processing
- 📄 **PDF Output** - Perfect for eBook readers
- 🚀 **Batch Download** - Grab entire chapters at once
- 🤖 **Auto Chapter Detection** - Smart URL parsing
- 📱 **Cross-Platform** - Works on any device
- 🆓 **Free Forever** - No hidden costs
- 🚫 **Ad-Free** - Zero interruptions
- ⚡ **Turbo Speeds** - Powered by Google Colab

---

## 🚀 Step-by-Step Guide

### 1️⃣ **Open Google Colab**
- Go to [Google Colab](https://colab.research.google.com)

- If you are on **Mobile** then open in **Desktop Mode** for better view

- Click **`File`** in the top menu → Select **`New Notebook`**

---

### 2️⃣ **Create Your First Code Cell**
- In your new notebook, you'll see a blank box with "Type code here" (this is a code cell)

- Click inside the box to activate it

---

### 3️⃣ **Code**
- **Copy paste this code in the first cell:**
```
!git clone https://github.com/Yui007/weebcentral_downloader
# Install required libraries
!pip install requests beautifulsoup4 selenium tqdm IPython ipywidgets img2pdf natsort
```
- **Copy paste this code in the second cell:**
```
%cd /content/weebcentral_downloader
!python weebcentral_scraper_colab.py
```
**Enter your manga URL from weebcentral.com after running this code**
- **Copy paste this code in the third cell:**
```
import os
import shutil
import img2pdf
from natsort import natsorted

output_dir = '/content/weebcentral_downloader/manga_downloads'

if os.path.exists(output_dir):
    manga_folders = [d for d in os.listdir(output_dir) if os.path.isdir(os.path.join(output_dir, d))]

    if manga_folders:
        print("Available manga folders:")
        for i, folder in enumerate(manga_folders, 1):
            print(f"{i}. {folder}")

        choice = int(input("\nEnter the number of the folder to process: ")) - 1
        if 0 <= choice < len(manga_folders):
            folder_name = manga_folders[choice]
            folder_path = os.path.join(output_dir, folder_name)

            # Process each chapter
            for chapter_dir in os.listdir(folder_path):
                chapter_path = os.path.join(folder_path, chapter_dir)
                if os.path.isdir(chapter_path):
                    images = []
                    # Collect all valid image files
                    for f in os.listdir(chapter_path):
                        if f.lower().endswith(('.png', '.jpg', '.jpeg')):
                            images.append(os.path.join(chapter_path, f))

                    if images:
                        # Natural sort images for proper order
                        images = natsorted(images)
                        pdf_path = os.path.join(folder_path, f"{chapter_dir}.pdf")

                        # Convert to PDF
                        with open(pdf_path, 'wb') as pdf_file:
                            pdf_file.write(img2pdf.convert(images))

                        # Cleanup images and empty folder
                        for img in images:
                            os.remove(img)
                        os.rmdir(chapter_path)
                        print(f"Converted: {chapter_dir} → {chapter_dir}.pdf")
                    else:
                        print(f"Skipped empty chapter: {chapter_dir}")

            # Zip optional
            if input("\nZip PDFs? (y/n): ").lower() == 'y':
                zip_path = f"/content/{folder_name}.zip"
                shutil.make_archive(f"/content/{folder_name}", 'zip', folder_path)
                print(f"\n✅ Zip created: {zip_path}")
            else:
                print("\nSkipped zip creation")
        else:
            print("Invalid selection!")
    else:
        print("No manga folders found!")
else:
    print("Download directory missing!")
```
### **Run all the cells in order**
---

### 4️⃣ **Download Your Manga**
- After final cell completes:
  1. Click 📁 **Files** icon in left sidebar
  2. Find **manga_output.pdf**
  3. Click ⬇️ download button next to file

---

# ⏳ Processing Time Varies
- 1 Chapter ≈ 1-2 minutes
- 10 Chapters ≈ 10-15 minutes
- **Never** interrupt cells mid-process

---

## 💡 Pro Tips
- For stuck cells: **Runtime → Restart runtime**
- Mobile users: Use desktop mode for full controls
- Need help? Screenshot error messages
- Close Colab tab after download to save resources

**Enjoy your manga reading!** 🎉
