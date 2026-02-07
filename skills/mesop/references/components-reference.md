# Components Reference

## Layout

### Box
Container for grouping and styling components. Flexbox/Grid powerhouse.
```python
with me.box(style=me.Style(display="flex", flex_direction="column", gap=16)):
  me.text("Item 1")
```

### Sidenav
Collapsible side navigation.
```python
with me.sidenav(opened=state.opened):
  me.text("Menu")
with me.box(style=me.Style(margin=me.Margin(left=state.sidenav_width))):
  me.slot()
```

### Divider
Horizontal line separator.
```python
me.divider()
```

## Inputs

### Input / Textarea
Text entry. Use `on_blur` for performance, `on_input` for real-time.
```python
me.input(label="Name", value=state.name, on_blur=on_blur)
me.textarea(label="Bio", value=state.bio, on_blur=on_blur)
```

### Select
Dropdown menu.
```python
me.select(
  label="Role",
  options=[me.SelectOption(label="Admin", value="admin"), me.SelectOption(label="User", value="user")],
  on_selection_change=on_change
)
```

### Checkbox / Radio / Slide Toggle
Boolean or single-choice selection.
```python
me.checkbox(label="Accept", checked=state.accepted, on_change=on_check)
me.radio(options=[...], on_change=on_radio)
me.slide_toggle(label="Dark Mode", on_change=on_toggle)
```

### Slider
Numeric range selection.
```python
me.slider(min=0, max=100, on_value_change=on_slider)
```

### Uploader
File upload component.
```python
me.uploader(
  label="Upload Image",
  accepted_file_types=["image/png", "image/jpeg"],
  on_upload=on_upload
)
```

## Action & Navigation

### Button
Clickable action.
```python
me.button("Submit", on_click=submit, type="raised", color="primary")
```

### Link
Hyperlink to external or internal URL.
```python
me.link(text="Google", url="https://google.com")
```

## Display

### Text
Basic text rendering.
```python
me.text("Hello World", type="headline-1")
```

### Markdown
Render Markdown content.
```python
me.markdown("# Title\nBody text")
```

### Image / Icon
Visual assets.
```python
me.image(src="https://example.com/img.png")
me.icon("home") # Material Symbols name
```

### Code
Code block with syntax highlighting.
```python
me.code("print('hello')", language="python")
```

### Table
Display Pandas DataFrame.
```python
me.table(dataframe, on_click=cell_click)
```

## Containers

### Card
Material design card with header, content, actions.
```python
with me.card():
  me.card_header(title="Title")
  with me.card_content():
    me.text("Content")
  with me.card_actions():
    me.button("Action")
```

### Expansion Panel
Collapsible accordion.
```python
with me.expansion_panel(title="Advanced Settings"):
  me.input(label="API Key")
```

## Feedback

### Progress
Loading indicators.
```python
me.progress_bar() # Linear
me.progress_spinner() # Circular
```

### Tooltip
Hover text.
```python
with me.tooltip(message="Help info"):
  me.icon("info")
```

## AI / Labs (`mesop.labs`)

### Chat
High-level chat interface.
```python
import mesop.labs as mel
mel.chat(transform_function, title="AI Chat", bot_user="Gemini")
```

### Text to Text / Image
Simple AI prompt-response UIs.
```python
mel.text_to_text(transform_function)
mel.text_to_image(transform_function)
```
