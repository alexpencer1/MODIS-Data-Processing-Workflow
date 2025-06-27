## (Phase 1) MODIS AOT Data Preparation – Step-by-Step Processing Guide 

This section outlines the **initial data preparation phase** required before processing MODIS Aerosol Optical Thickness (AOT) data. It focuses on organizing downloaded data, verifying file completeness, and preparing for further analysis.

---

### 1. Assumption: Data Access and Download

It is assumed that the user already has access to NASA's LAADS DAAC through the website "[https://ladsweb.modaps.eosdis.nasa.gov/" ](https://ladsweb.modaps.eosdis.nasa.gov/%22%22or) and has successfully downloaded MODIS AOT data  in HDF4 format else visit here or check out MODIS AOT ACCESS AND DOWNLOAD repository

---

### 2. Organize Downloaded Files

* Save all downloaded MODIS `.hdf` files in a dedicated folder.
* Alongside these files, a metadata file named something like `checksum_xxxxxxxxx.htm` is usually provided.
* This **checksum file** lists all expected `.hdf` files and serves as a reference to verify that the download is complete.

---

### 3. Generate File List Using Command Prompt

To create a list of all downloaded HDF files:

1. Open **Command Prompt** and navigate to the directory containing the MODIS data using:

   ```cmd
   cd /d D:\Path\To\Your\MODIS\Folder
   ```

2. List the files to verify presence:

   ```cmd
   dir or ls
   ```

3. Create a simple list of all `.hdf` files in the folder:

   ```cmd
   dir /b *.hdf > fileList.txt
   ```

4. Verify that the new file `fileList.txt` was created:

   ```cmd
   dir or ls
   ```

5. Optionally, open the `fileList.txt` using Notepad or any text editor to confirm it contains only the `.hdf` filenames.

---

### 4. Create a Verification Folder

* Create a new folder called `check` anywhere convenient (e.g., Desktop).
* Copy both the `checksum_xxxxxxxxx.htm` file and `fileList.txt` into this new `check` folder.

---

### 5. Run the MODIS Checksum Verification Code – Part 1

This Python script compares the listed `.hdf` files in `fileList.txt` against the official `checksum` HTML file.

#### ➤ Modify the following lines in the script:

```python
html_file_path = r"C:\Users\YourUsername\Desktop\check\checksums_502376085.htm"
output_file_path = r"C:\Users\YourUsername\Desktop\check\fileList.txt"
```

Run the code. If successful, you should see:

```
Filenames saved to C:\Users\YourUsername\Desktop\check\fileList.txt
```

---

### 6. Run the MODIS Checksum Verification Code – Part 2

This section validates the actual `.hdf` files downloaded against the expected files using the `fileList.txt`.

#### ➤ Modify the following variables in the second section of the code:

```python
directory = r"D:\ARTICLE 1\NIGERIA MODIS\2012_2013"  # Folder with .hdf files
file_list_path = r"C:\Users\YourUsername\Desktop\check\fileList.txt"  # File list path
```

#### ➤ Run the script:

* If all expected files were downloaded, the result will be:

  ```
  Total expected files: 1870
  Total downloaded files: 1872
  Total missing files: 0

  All files are downloaded successfully.
  ```

* If files are missing, the script will report:

  * Number of expected files
  * Number of downloaded files
  * Number of missing files
  * The filenames of missing files for easy identification and redownload

---

### ✅ Summary

This step concludes the **data integrity verification phase**, ensuring you are working with a complete and valid MODIS dataset before proceeding to extraction, analysis, and validation.
