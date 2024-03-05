# gordenda

A simple file uploader package for Node.js and Express.js.

## Installation

You can install gordenda using npm:

```
npm install gordenda
```

## Usage

```javascript
const express = require('express');
const multer = require('multer');
const gordenda = require('gordenda');

const app = express();
const port = process.env.PORT || 3000;

// Set up multer storage for uploaded files
const storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, 'uploads/')
  },
  filename: function (req, file, cb) {
    cb(null, Date.now() + '-' + file.originalname)
  }
});

const upload = multer({ storage: storage });

// Serve the HTML form for uploading files
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'index.html'));
});

// Handle file upload POST request
app.post('/upload', upload.single('file'), (req, res) => {
  if (!req.file) {
    return res.status(400).send('No files were uploaded.');
  }
  res.send('File uploaded successfully.');
});

// Start the server
app.listen(port, () => {
  console.log(`Server is listening on port ${port}`);
});
```

## Dependencies

- [express](https://www.npmjs.com/package/express): Fast, unopinionated, minimalist web framework for Node.js
- [multer](https://www.npmjs.com/package/multer): Middleware for handling `multipart/form-data`, which is primarily used for uploading files.

## License

MIT
