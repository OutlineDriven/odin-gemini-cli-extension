# Core Patterns

## State Management

Mesop uses a unique approach to state management where state is scoped to the user session and stored in a dataclass.

### Defining State

Use `@me.stateclass` to define the state structure. This behaves like a standard Python dataclass but handles serialization between server and client.

```python
import mesop as me
from dataclasses import field

@me.stateclass
class State:
  # Primitive types (int, float, str, bool)
  count: int = 0
  
  # Collections (list, dict, set) - MUST use immutable default or factory
  items: list[str] = field(default_factory=list)
  
  # Nested state (dataclasses)
  user: UserProfile | None = None
```

**Rules:**
1.  **Serializable**: All fields must be serializable (primitives, collections, dataclasses, Pydantic models, Pandas DataFrames).
2.  **Immutable Defaults**: Never use mutable defaults like `list = []`. Use `field(default_factory=list)` instead.
3.  **No Global State**: Do not use global variables for user state; they will leak across sessions.

### Accessing State

Access state within components or event handlers using `me.state(StateClass)`.

```python
def button_click(e: me.ClickEvent):
  state = me.state(State)
  state.count += 1
```

## Event Handlers

Event handlers respond to user interactions. They can be regular functions, generators (for streaming), or async functions.

### Regular Handlers
Run to completion before updating the UI.

```python
def on_click(e: me.ClickEvent):
  state = me.state(State)
  state.count += 1
```

### Generator Handlers (Streaming)
Yield control to the framework to update the UI incrementally. Useful for loading states or streaming responses.

**Critical Rule**: Must `yield` at the end of the function to ensure final state update.

```python
import time

def on_click(e: me.ClickEvent):
  state = me.state(State)
  state.loading = True
  yield # Render loading state
  
  # Simulate work
  time.sleep(2)
  
  state.loading = False
  yield # Render final state
```

### Async Handlers
Use `async` and `await` for concurrent operations. Can also be generators (`async def` + `yield`).

```python
import asyncio

async def on_click(e: me.ClickEvent):
  state = me.state(State)
  state.result = await fetch_data()
  yield
```

## Navigation & Routing

### Page Definition
Define pages using the `@me.page` decorator.

```python
@me.page(path="/")
def home():
  me.text("Home")

@me.page(path="/settings")
def settings():
  me.text("Settings")
```

### Navigation Command
Navigate programmatically using `me.navigate`.

```python
def go_home(e: me.ClickEvent):
  me.navigate("/")
```

### Query Parameters
Read and write query parameters using `me.query_params`.

```python
# Reading
def page():
  q = me.query_params.get("q", "default")

# Writing/Navigating with params
def search(e: me.ClickEvent):
  me.navigate("/search", query_params={"q": "mesop"})
```

## Viewport & Scrolling

### Responsive Design
Use `me.viewport_size()` to adapt layouts based on screen size.

```python
@me.page()
def page():
  is_mobile = me.viewport_size().width < 640
  with me.box(style=me.Style(flex_direction="column" if is_mobile else "row")):
    ...
```

### Scroll Into View
Scroll a specific component into view using its key.

```python
me.box(key="target-box")
# ...
me.scroll_into_view(key="target-box")
```

### Focus Component
Focus an input or other focusable element.

```python
me.input(key="main-input")
# ...
me.focus_component(key="main-input")
```

## Lifecycle Events

### On Load
Run logic when a page loads (e.g., fetch initial data).

```python
def on_load(e: me.LoadEvent):
  state = me.state(State)
  state.data = load_data()

@me.page(on_load=on_load)
def page():
  ...
```
