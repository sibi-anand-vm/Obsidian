### Overview:

1. **Reboot**: Overrides browser default styles to ensure consistency.
2. **Display Classes**: `display-1` to `display-6` for large headings.
3. **Text Properties**: Utilities like `text-center`, `fw-bold`, `text-decoration`.
4. **Colors**: Predefined colours like `text-primary`, `bg-success`, `btn-danger`.
5. **Buttons**: Classes like `btn-primary`, `btn-lg`, and `btn-group`.
6. **Margin and Padding**: Utilities like `m-3`, `p-4`.
7. **Borders and Shadows**: Classes like `border`, `shadow-lg`.
8. **Container and Grid**: Responsive containers and the 12-column grid system.

### Sample Code:
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Bootstrap Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
  <!-- Container -->
  <div class="container-fluid bg-light p-4">
    <!-- Reboot and Display -->
    <h1 class="display-1 text-center text-primary">Welcome to Bootstrap</h1>
    <p class="lead text-center">This is a simple demonstration of Bootstrap features.</p>
    
    <!-- Colors and Text Properties -->
    <div class="text-center">
      <p class="text-success fw-bold">This text is styled with Bootstrap colors and weight.</p>
      <p class="text-danger text-decoration-underline">Dangerous text with an underline!</p>
    </div>
    
    <!-- Buttons -->
    <div class="text-center">
      <button class="btn btn-primary btn-lg m-2">Primary Button</button>
      <button class="btn btn-secondary btn-sm m-2">Secondary Button</button>
      <div class="btn-group mt-3">
        <button class="btn btn-success">Option 1</button>
        <button class="btn btn-warning">Option 2</button>
        <button class="btn btn-danger">Option 3</button>
      </div>
    </div>
    
    <!-- Grid System -->
    <div class="container mt-4">
      <div class="row">
        <div class="col-md-4 p-3 border">Column 1</div>
        <div class="col-md-4 p-3 border">Column 2</div>
        <div class="col-md-4 p-3 border">Column 3</div>
      </div>
    </div>
    
    <!-- Borders, Shadows, and Margin/Padding -->
    <div class="mt-4 p-4 border border-dark shadow-lg text-center">
      <h2 class="display-4">Borders and Shadows</h2>
      <p class="m-3">This box has a border and shadow applied using Bootstrap classes.</p>
    </div>
  </div>

  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>

```

### Features Included:

- **Reboot**: Consistent styles.
- **Display Classes**: `display-1` and `display-4`.
- **Text Properties**: `text-center`, `fw-bold`, `text-decoration-underline`.
- **Colors**: `text-primary`, `text-success`, `text-danger`.
- **Buttons**: Various sizes, colors, and a `btn-group`.
- **Grid System**: A 12-column grid with three equal columns.
- **Borders and Shadows**: Example of `border` and `shadow-lg`.
- **Margin and Padding**: Classes like `m-3`, `p-4`.