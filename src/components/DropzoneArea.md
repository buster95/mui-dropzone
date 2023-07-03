### Import

```jsx static
import { DropzoneArea } from "material-ui-dropzone";
```

### Basic usage

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneArea onChange={(files) => console.log("Files:", files)} />
</ThemeProvider>;
```

### Accept only images

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

<ThemeProvider theme={theme}>
  <DropzoneArea
    acceptedFiles={["image/*"]}
    dropzoneText={"Drag and drop an image here or click"}
    onChange={(files) => console.log("Files:", files)}
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

<ThemeProvider theme={theme}>
  <DropzoneArea getPreviewIcon={handlePreviewIcon} />
</ThemeProvider>;
```

### Loading initial files

```jsx
import { ThemeProvider, createTheme } from "@mui/material";

const theme = createTheme();

const file = new File(["foo"], "foo.txt", {
  type: "text/plain",
});

<ThemeProvider theme={theme}>
  <DropzoneArea
    initialFiles={[file]}
    onChange={(files) => console.log("Files:", files)}
  />
</ThemeProvider>;
```

### Using chips for preview

Chips use the Grid system as well, so you can customize the way they appears and benefit from the Material-UI grid customizations

```jsx
import { ThemeProvider, createTheme } from "@mui/material";
import { createStyles, makeStyles } from "@mui/styles";

const theme = createTheme();
const useStyles = makeStyles((theme) =>
  createStyles({
    previewChip: {
      minWidth: 160,
      maxWidth: 210,
    },
  })
);

const classes = useStyles();

<ThemeProvider theme={theme}>
  <DropzoneArea
    showPreviews={true}
    showPreviewsInDropzone={false}
    useChipsForPreview
    previewGridProps={{ container: { spacing: 1, direction: "row" } }}
    previewChipProps={{ classes: { root: classes.previewChip } }}
    previewText="Selected files"
  />
</ThemeProvider>;
```
