
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>GETUNZIPPED!</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
   
    body {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: #333;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }
   
    .card {
      background: rgba(255, 255, 255, 0.95);
      border-radius: 16px;
      padding: 30px;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);
      width: 800px;
      max-width: 95%;
      backdrop-filter: blur(10px);
    }
   
    header {
      text-align: center;
      margin-bottom: 25px;
      padding-bottom: 20px;
      border-bottom: 1px solid rgba(0, 0, 0, 0.1);
    }
   
    h1 {
      font-size: 28px;
      margin-bottom: 8px;
      background: linear-gradient(to right, #667eea, #764ba2);
      -webkit-background-clip: text;
      background-clip: text;
      color: transparent;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 12px;
    }
   
    .subtitle {
      color: #666;
      font-size: 16px;
    }
   
    .upload-section {
      margin-bottom: 25px;
    }
   
    .file-input-wrapper {
      position: relative;
      display: inline-block;
      width: 100%;
    }
   
    .file-input-label {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      padding: 30px;
      border: 3px dashed #667eea;
      border-radius: 12px;
      background: rgba(102, 126, 234, 0.05);
      cursor: pointer;
      transition: all 0.3s;
      text-align: center;
    }
   
    .file-input-label:hover {
      background: rgba(102, 126, 234, 0.1);
      border-color: #764ba2;
    }
   
    .file-input-label.dragover {
      background: rgba(102, 126, 234, 0.2);
      border-color: #5a67d8;
      transform: scale(1.02);
    }
   
    .upload-icon {
      font-size: 48px;
      color: #667eea;
      margin-bottom: 15px;
    }
   
    .upload-text {
      font-size: 18px;
      color: #667eea;
      margin-bottom: 8px;
      font-weight: 600;
    }
   
    .upload-subtext {
      color: #666;
      margin-bottom: 15px;
    }
   
    .browse-btn {
      background: linear-gradient(to right, #667eea, #764ba2);
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 50px;
      font-weight: 600;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
      box-shadow: 0 5px 15px rgba(102, 126, 234, 0.4);
    }
   
    .browse-btn:hover {
      transform: translateY(-3px);
      box-shadow: 0 8px 20px rgba(102, 126, 234, 0.6);
    }
   
    #fileInput {
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0;
      left: 0;
      opacity: 0;
      cursor: pointer;
    }
   
    .controls {
      display: flex;
      gap: 12px;
      margin-top: 20px;
      flex-wrap: wrap;
    }
   
    .action-btn {
      flex: 1;
      min-width: 200px;
      padding: 14px 20px;
      border-radius: 10px;
      border: none;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }
   
    .action-btn.primary {
      background: linear-gradient(to right, #667eea, #764ba2);
      color: white;
    }
   
    .action-btn.success {
      background: linear-gradient(to right, #48bb78, #38a169);
      color: white;
    }
   
    .action-btn:hover:not(:disabled) {
      transform: translateY(-3px);
      box-shadow: 0 6px 18px rgba(0, 0, 0, 0.15);
    }
   
    .action-btn:disabled {
      background: #a0aec0;
      color: #718096;
      cursor: not-allowed;
      transform: none;
      box-shadow: none;
    }
   
    #status {
      margin-top: 15px;
      padding: 12px 16px;
      border-radius: 8px;
      background: #f7fafc;
      border-left: 4px solid #667eea;
      font-size: 14px;
      color: #4a5568;
    }
   
    .file-list-container {
      margin-top: 20px;
      max-height: 400px;
      overflow: auto;
      border-radius: 12px;
      padding: 5px;
      background: #f8fafc;
      border: 1px solid #e2e8f0;
    }
   
    #fileList {
      display: flex;
      flex-direction: column;
      gap: 2px;
    }
   
    .item {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 12px 16px;
      border-radius: 8px;
      background: white;
      transition: background 0.2s;
      word-break: break-all;
    }
   
    .item:hover {
      background: #edf2f7;
    }
   
    .item:not(:last-child) {
      border-bottom: 1px dashed #e2e8f0;
    }
   
    .file-info {
      display: flex;
      align-items: center;
      gap: 12px;
      flex: 1;
    }
   
    .file-icon {
      color: #667eea;
      font-size: 18px;
      width: 24px;
      text-align: center;
    }
   
    .file-name {
      font-weight: 500;
    }
   
    .file-actions {
      display: flex;
      gap: 8px;
    }
   
    .file-btn {
      padding: 6px 12px;
      border-radius: 6px;
      border: 1px solid #cbd5e0;
      background: white;
      cursor: pointer;
      font-size: 13px;
      transition: all 0.2s;
    }
   
    .file-btn:hover {
      background: #667eea;
      color: white;
      border-color: #667eea;
    }
   
    .folder-tag {
      display: inline-block;
      background: rgba(102, 126, 234, 0.1);
      color: #667eea;
      padding: 2px 8px;
      border-radius: 12px;
      font-size: 12px;
      margin-left: 8px;
    }
   
    .tip {
      margin-top: 15px;
      font-size: 13px;
      color: #718096;
      text-align: center;
      padding: 10px;
      background: rgba(102, 126, 234, 0.05);
      border-radius: 8px;
    }

    .footer {
      text-align: center;
      margin-top: 20px;
      font-size: 14px;
      color: #666;
      font-weight: 500;
    }

    .heart {
      color: #e53e3e;
    }
   
    .progress-bar {
      height: 6px;
      background: #e2e8f0;
      border-radius: 3px;
      overflow: hidden;
      margin-top: 10px;
      display: none;
    }
   
    .progress {
      height: 100%;
      background: linear-gradient(to right, #667eea, #764ba2);
      width: 0%;
      transition: width 0.3s;
    }
   
    @media (max-width: 600px) {
      .card {
        padding: 20px;
      }
     
      h1 {
        font-size: 24px;
      }
     
      .controls {
        flex-direction: column;
      }
     
      .action-btn {
        min-width: 100%;
      }
     
      .item {
        flex-direction: column;
        align-items: flex-start;
        gap: 10px;
      }
     
      .file-actions {
        align-self: flex-end;
      }
    }
  </style>
</head>
<body>
  <div class="card">
    <header>
      <h1><i class="fas fa-file-archive"></i> GETUNZIPPED!</h1>
      <p class="subtitle">Extract, preview, and download files from ZIP archives</p>
    </header>
   
    <div class="upload-section">
      <div class="file-input-wrapper">
        <label for="fileInput" class="file-input-label" id="fileInputLabel">
          <div class="upload-icon">
            <i class="fas fa-file-upload"></i>
          </div>
          <div class="upload-text">Drop your ZIP file here</div>
          <div class="upload-subtext">or click to browse your files</div>
          <button class="browse-btn">Browse Files</button>
        </label>
        <input id="fileInput" type="file" accept=".zip" />
      </div>
     
      <div class="controls">
        <button id="downloadAllBtn" class="action-btn primary" disabled>
          <i class="fas fa-download"></i> Download All (as ZIP)
        </button>
        <button id="saveToFolderBtn" class="action-btn success" disabled>
          <i class="fas fa-folder-open"></i> Save to Folder
        </button>
      </div>
     
      <div id="status">Upload a .zip file to see contents.</div>
     
      <div class="progress-bar" id="progressBar">
        <div class="progress" id="progress"></div>
      </div>
    </div>
   
    <div class="file-list-container">
      <div id="fileList">No file loaded.</div>
    </div>
   
    <div class="tip">
      <i class="fas fa-lightbulb"></i> Tip: Use "Save to Folder" to write files directly into a chosen folder (Chromium browsers only).
    </div>

    <footer class="footer">
      Made with <span class="heart">❤</span> for Pooja
    </footer>
  </div>

  <!-- Reliable CDN for JSZip -->
  <script src="https://cdn.jsdelivr.net/npm/jszip@3.10.1/dist/jszip.min.js"></script>
  <script>
    const fileInput = document.getElementById('fileInput');
    const fileInputLabel = document.getElementById('fileInputLabel');
    const fileList = document.getElementById('fileList');
    const status = document.getElementById('status');
    const downloadAllBtn = document.getElementById('downloadAllBtn');
    const saveToFolderBtn = document.getElementById('saveToFolderBtn');
    const progressBar = document.getElementById('progressBar');
    const progress = document.getElementById('progress');

    let currentZip = null;
    let fileEntries = []; // {name: normalizedPath, getBlob: ()=>Promise<Blob>}

    // Normalize names: convert backslashes to forward, remove leading './'
    function normalizePath(name){
      return name.replace(/\\+/g, '/').replace(/^\.\//, '');
    }

    // Set up drag and drop
    fileInputLabel.addEventListener('dragover', (e) => {
      e.preventDefault();
      fileInputLabel.classList.add('dragover');
    });

    fileInputLabel.addEventListener('dragleave', () => {
      fileInputLabel.classList.remove('dragover');
    });

    fileInputLabel.addEventListener('drop', (e) => {
      e.preventDefault();
      fileInputLabel.classList.remove('dragover');
     
      if (e.dataTransfer.files.length) {
        fileInput.files = e.dataTransfer.files;
        handleFileUpload();
      }
    });

    fileInput.addEventListener('change', handleFileUpload);

    async function handleFileUpload() {
      const f = fileInput.files?.[0];
      resetState();
      if (!f) return;
     
      // Check if file is a ZIP
      if (!f.name.toLowerCase().endsWith('.zip')) {
        status.textContent = 'Please select a valid ZIP file.';
        status.style.borderLeftColor = '#e53e3e';
        return;
      }
     
      status.textContent = 'Loading ZIP file...';
      status.style.borderLeftColor = '#667eea';
      fileList.innerHTML = '';
     
      try {
        const ab = await f.arrayBuffer();
        const zip = await JSZip.loadAsync(ab);
        currentZip = zip;

        // Build and sort names for stable order
        const rawNames = Object.keys(zip.files || {});
        if (!rawNames.length) {
          status.textContent = 'The ZIP file is empty.';
          return;
        }

        // Normalize names and map back to zip.files entry
        const entries = rawNames.map(n => {
          return { rawName: n, normName: normalizePath(n), entry: zip.files[n] };
        });

        // Sort so folders come before files in UI (optional)
        entries.sort((a,b) => a.normName.localeCompare(b.normName, undefined, {sensitivity:'base'}));

        // Populate UI and fileEntries list (skip pure folder entries)
        let countFiles = 0;
        entries.forEach(obj => {
          const name = obj.normName;
          const entry = obj.entry;

          // Some ZIPs use backslashes in names; we've normalized above.
          // Treat as directory if entry.dir === true OR name ends with '/'
          const isDir = entry.dir || name.endsWith('/');

          const div = document.createElement('div');
          div.className = 'item';
         
          const fileInfo = document.createElement('div');
          fileInfo.className = 'file-info';
         
          const fileIcon = document.createElement('div');
          fileIcon.className = 'file-icon';
          fileIcon.innerHTML = isDir ? '<i class="fas fa-folder"></i>' : '<i class="fas fa-file"></i>';
         
          const fileName = document.createElement('div');
          fileName.className = 'file-name';
          fileName.textContent = name;
         
          fileInfo.appendChild(fileIcon);
          fileInfo.appendChild(fileName);
         
          if (isDir) {
            const folderTag = document.createElement('span');
            folderTag.className = 'folder-tag';
            folderTag.textContent = 'folder';
            fileInfo.appendChild(folderTag);
          }
         
          const fileActions = document.createElement('div');
          fileActions.className = 'file-actions';

          if (!isDir) {
            countFiles++;
            const dbtn = document.createElement('button');
            dbtn.className = 'file-btn';
            dbtn.innerHTML = '<i class="fas fa-download"></i> Download';
            dbtn.onclick = async () => {
              try {
                status.textContent = `Preparing ${name}...`;
                const blob = await entry.async('blob');
                triggerDownload(blob, name.split('/').pop() || name);
                status.textContent = 'Ready.';
              } catch (err) {
                console.error(err);
                status.textContent = 'Failed to prepare file.';
                status.style.borderLeftColor = '#e53e3e';
              }
            };
            fileActions.appendChild(dbtn);

            // store getter that returns blob when needed; use closure of entry
            fileEntries.push({
              name, // preserve normalized path including folders
              getBlob: () => entry.async('blob')
            });
          }

          div.appendChild(fileInfo);
          div.appendChild(fileActions);
          fileList.appendChild(div);
        });

        status.textContent = `Loaded ${countFiles} file(s) from the ZIP archive.`;
        downloadAllBtn.disabled = countFiles === 0;
        saveToFolderBtn.disabled = (typeof window.showDirectoryPicker !== 'function') || countFiles === 0;

      } catch (err) {
        console.error(err);
        status.textContent = 'Error reading ZIP file. Ensure the file is a valid .zip archive.';
        status.style.borderLeftColor = '#e53e3e';
        fileList.innerHTML = '';
      }
    }

    // Utility: create anchor and trigger download, revoke after short delay
    function triggerDownload(blob, filename) {
      const url = URL.createObjectURL(blob);
      const a = document.createElement('a');
      a.style.display = 'none';
      a.href = url;
      a.download = filename || 'file';
      document.body.appendChild(a);
      a.click();
      // In some browsers revoking too early breaks the download. Revoke after 1s.
      setTimeout(() => {
        URL.revokeObjectURL(url);
        a.remove();
      }, 1000);
    }

    // Repack all files into a single ZIP and download once
    downloadAllBtn.addEventListener('click', async () => {
      if (!fileEntries.length) return;
      downloadAllBtn.disabled = true;
      saveToFolderBtn.disabled = true;
      status.textContent = 'Repacking files into single ZIP...';
      progressBar.style.display = 'block';
      progress.style.width = '0%';

      try {
        const outZip = new JSZip();

        // add all files preserving folder structure
        for (let i = 0; i < fileEntries.length; i++) {
          const e = fileEntries[i];
          status.textContent = `Adding (${i+1}/${fileEntries.length}): ${e.name}`;
          progress.style.width = `${(i / fileEntries.length) * 100}%`;
         
          // get blob
          const blob = await e.getBlob();
          // JSZip.file path must use forward slashes; we already normalized
          outZip.file(e.name, blob);
        }

        status.textContent = 'Generating final ZIP...';
        progress.style.width = '100%';
       
        const blobOut = await outZip.generateAsync({ type: 'blob', compression: 'DEFLATE' }, meta => {
          // show percent if available
          if (meta && typeof meta.percent === 'number') {
            status.textContent = `Generating final ZIP: ${Math.round(meta.percent)}%`;
          }
        });

        triggerDownload(blobOut, 'all-files-extracted.zip');
        status.textContent = 'Downloaded all files as all-files-extracted.zip';
        status.style.borderLeftColor = '#38a169';
      } catch (err) {
        console.error(err);
        status.textContent = 'Error while creating the combined ZIP.';
        status.style.borderLeftColor = '#e53e3e';
      } finally {
        downloadAllBtn.disabled = false;
        saveToFolderBtn.disabled = (typeof window.showDirectoryPicker !== 'function') || fileEntries.length === 0;
        progressBar.style.display = 'none';
      }
    });

    // Save all files into a folder chosen by user (File System Access API)
    saveToFolderBtn.addEventListener('click', async () => {
      if (typeof window.showDirectoryPicker !== 'function') {
        alert('File System Access API not supported in this browser. Try using Google Chrome or Microsoft Edge.');
        return;
      }
      if (!fileEntries.length) return;

      saveToFolderBtn.disabled = true;
      downloadAllBtn.disabled = true;
      status.textContent = 'Please choose a folder...';
      progressBar.style.display = 'block';
      progress.style.width = '0%';

      try {
        const dirHandle = await window.showDirectoryPicker();
        status.textContent = 'Saving files to chosen folder...';

        for (let i = 0; i < fileEntries.length; i++) {
          const e = fileEntries[i];
          status.textContent = `Writing (${i+1}/${fileEntries.length}): ${e.name}`;
          progress.style.width = `${(i / fileEntries.length) * 100}%`;
         
          // Create subdirectories as needed
          const parts = e.name.split('/').filter(p => p !== '');
          const fileName = parts.pop();
          let curDir = dirHandle;
          for (const p of parts) {
            curDir = await curDir.getDirectoryHandle(p, { create: true });
          }
          const fh = await curDir.getFileHandle(fileName, { create: true });
          const writable = await fh.createWritable();
          const blob = await e.getBlob();
          await writable.write(blob);
          await writable.close();
        }

        progress.style.width = '100%';
        status.textContent = 'All files saved to folder successfully.';
        status.style.borderLeftColor = '#38a169';
      } catch (err) {
        console.error(err);
        if (err.name === 'AbortError') {
          status.textContent = 'Save to folder cancelled.';
        } else {
          status.textContent = 'Save to folder failed.';
        }
        status.style.borderLeftColor = '#e53e3e';
      } finally {
        saveToFolderBtn.disabled = false;
        downloadAllBtn.disabled = false;
        progressBar.style.display = 'none';
      }
    });

    function resetState(){
      currentZip = null;
      fileEntries = [];
      downloadAllBtn.disabled = true;
      saveToFolderBtn.disabled = true;
      fileList.innerHTML = 'No file loaded.';
      status.textContent = 'Upload a .zip file to see contents.';
      status.style.borderLeftColor = '#667eea';
      progressBar.style.display = 'none';
    }
  </script>
</body>
</html>
