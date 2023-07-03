### Import

```jsx static
import { DropzoneAreaBase } from "material-ui-dropzone";
```

### Basic usage

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    onAdd={(fileObjs) => console.log("Added Files:", fileObjs)}
    onDelete={(fileObj) => console.log("Removed File:", fileObj)}
    onAlert={(message, variant) => console.log(`${variant}: ${message}`)}
  />
</ThemeProvider>;
```

### Accept only images

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    acceptedFiles={["image/*"]}
    dropzoneText={"Drag and drop an image here or click"}
    onChange={(files) => console.log("Files:", files)}
    onAlert={(message, variant) => console.log(`${variant}: ${message}`)}
  />
</ThemeProvider>;
```

### Custom Dropzone Icon

```jsx
import { ThemeProvider, createTheme } from "@mui/material";
import { AttachFile } from "@mui/icons-material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    Icon={AttachFile}
    dropzoneText={"Drag and drop an image here or click"}
    onChange={(files) => console.log("Files:", files)}
    onAlert={(message, variant) => console.log(`${variant}: ${message}`)}
  />
</ThemeProvider>;
```

### Reset button

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    onAdd={(fileObjs) => console.log("Added Files:", fileObjs)}
    onDelete={(fileObj) => console.log("Removed File:", fileObj)}
    onAlert={(message, variant) => console.log(`${variant}: ${message}`)}
    reset={{
      onClick: () => console.log("reset"),
    }}
  />
</ThemeProvider>;
```

### Custom reset button

Allow to pass any valid DOM node valid to react to use custom reset button

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    onAdd={(fileObjs) => console.log("Added Files:", fileObjs)}
    onDelete={(fileObj) => console.log("Removed File:", fileObj)}
    onAlert={(message, variant) => console.log(`${variant}: ${message}`)}
    reset={
      <button style={{ margin: "20px 0" }} onClick={() => console.log("reset")}>
        reset
      </button>
    }
  />
</ThemeProvider>;
```

### Custom Preview Icon

Demonstration of how to customize the preview icon for:

- PDF files
- Video
- Audio
- Word Documents

```jsx
import React, { useState } from "react";

import { ThemeProvider, createTheme } from "@mui/material";
import {
  AttachFile,
  AudioTrack,
  Description,
  PictureAsPdf,
  Theaters,
} from "@mui/icons-material";

const theme = createTheme();

const handlePreviewIcon = (fileObject, classes) => {
  const { type } = fileObject.file;
  const iconProps = {
    className: classes.image,
  };

  if (type.startsWith("video/")) return <Theaters {...iconProps} />;
  if (type.startsWith("audio/")) return <AudioTrack {...iconProps} />;

  switch (type) {
    case "application/msword":
    case "application/vnd.openxmlformats-officedocument.wordprocessingml.document":
      return <Description {...iconProps} />;
    case "application/pdf":
      return <PictureAsPdf {...iconProps} />;
    default:
      return <AttachFile {...iconProps} />;
  }
};

const [fileObjects, setFileObjects] = useState([]);

<ThemeProvider theme={theme}>
  <DropzoneAreaBase
    fileObjects={fileObjects}
    onAdd={(newFileObjs) => {
      console.log("onAdd", newFileObjs);
      setFileObjects([].concat(fileObjects, newFileObjs));
    }}
    onDelete={(deleteFileObj) => {
      console.log("onDelete", deleteFileObj);
    }}
    getPreviewIcon={handlePreviewIcon}
  />
</ThemeProvider>;
```
