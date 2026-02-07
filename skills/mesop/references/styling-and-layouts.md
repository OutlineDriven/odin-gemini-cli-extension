# Styling and Layouts

Mesop provides a Pythonic API for CSS styling and layout, primarily through `me.Style` and the `me.box` component.

## The Style Object

The `me.Style` dataclass exposes CSS properties as Python arguments. Keys are generally snake_case versions of CSS properties.

```python
style = me.Style(
  background_color="blue",
  color="white",
  padding=me.Padding.all(16),
  border_radius=8,
  font_weight="bold"
)
```

## Box Layout (Flexbox)

The primary layout mechanism is Flexbox, configured via `me.box`.

### Row (Horizontal)
```python
with me.box(style=me.Style(display="flex", flex_direction="row", gap=16)):
  me.box(style=me.Style(flex_grow=1, background="red"))
  me.box(style=me.Style(width=100, background="blue"))
```

### Column (Vertical)
```python
with me.box(style=me.Style(display="flex", flex_direction="column", align_items="center")):
  me.text("Title")
  me.text("Subtitle")
```

## Grid Layout

CSS Grid is also fully supported.

```python
with me.box(style=me.Style(
  display="grid",
  grid_template_columns="1fr 2fr", # Two columns, second is 2x wider
  gap=16
)):
  me.text("Sidebar")
  me.text("Main Content")
```

## Helpers

### Margin & Padding
Use helpers for concise spacing definitions.

- `me.Padding.all(16)` -> 16px on all sides
- `me.Padding.symmetric(vertical=10, horizontal=20)`
- `me.Margin.only(top=5, bottom=5)`

### Border
- `me.Border.all(me.BorderSide(width=1, color="black", style="solid"))`
- `me.Border.symmetric(horizontal=me.BorderSide(...))`

## Theming

Mesop supports light and dark modes (Material Design 3).

### Setting Theme Mode
```python
# Typically in on_load
def on_load(e: me.LoadEvent):
  me.set_theme_mode("system") # or "light", "dark"
```

### Using Theme Variables
Reference theme colors that adapt to the mode.
```python
style=me.Style(
  background=me.theme_var("surface-container"),
  color=me.theme_var("on-surface")
)
```

Common vars: `primary`, `on-primary`, `surface`, `on-surface`, `background`, `outline`.

## Responsive Design

Adapt layouts based on viewport size.

```python
@me.page()
def page():
  is_mobile = me.viewport_size().width < 600
  
  with me.box(style=me.Style(
    flex_direction="column" if is_mobile else "row"
  )):
    ...
```

## Tailwind CSS

You can load external stylesheets and use class names.

1.  **Load Stylesheet**:
    ```python
    @me.page(stylesheets=["https://.../tailwind.min.css"])
    ```
2.  **Use Classes**:
    ```python
    me.box(classes="bg-blue-500 p-4 rounded-lg")
    ```
