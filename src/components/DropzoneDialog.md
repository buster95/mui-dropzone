### Import

```jsx static
import { DropzoneDialog } from "material-ui-dropzone";
```

### Basic usage

```jsx
import { ThemeProvider, createTheme } from "@mui/material";
import Button from "@mui/material/Button";

const theme = createTheme();

const [open, setOpen] = React.useState(false);

<ThemeProvider theme={theme}>
  <div>
    <Button variant="contained" color="primary" onClick={() => setOpen(true)}>
      Add Image
    </Button>

    <DropzoneDialog
      acceptedFiles={["image/*"]}
      cancelButtonText={"cancel"}
      submitButtonText={"submit"}
      maxFileSize={5000000}
      open={open}
      onClose={() => setOpen(false)}
      onSave={(files) => {
        console.log("Files:", files);
        setOpen(false);
      }}
      showPreviews={true}
      showFileNamesInPreview={true}
    />
  </div>
</ThemeProvider>;
```
