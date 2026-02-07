# Web Components

Mesop allows integrating custom JavaScript via Web Components (Lit) for functionality not available in native components or for client-side interactivity.

## Anatomy

A web component consists of a Python module (interface) and a JavaScript module (implementation).

### Python Module
```python
import mesop as me
from typing import Any, Callable

@me.web_component(path="./counter.js")
def counter(
  *,
  value: int,
  on_change: Callable[[me.WebEvent], Any],
  key: str | None = None,
):
  return me.insert_web_component(
    name="my-counter", # Must match customElement name in JS
    key=key,
    events={"changeEvent": on_change}, # Map JS event prop to Python handler
    properties={"value": value},       # Pass props to JS
  )
```

### JavaScript Module (Lit)
```javascript
import {LitElement, html} from 'https://cdn.jsdelivr.net/gh/lit/dist@3/core/lit-core.min.js';

class Counter extends LitElement {
  static properties = {
    value: {type: Number},
    changeEvent: {type: String}, // Event ID passed from Python
  };

  render() {
    return html`
      <button @click="${this._onClick}">Count is ${this.value}</button>
    `;
  }

  _onClick() {
    // Dispatch MesopEvent to call Python handler
    this.dispatchEvent(new MesopEvent(this.changeEvent, {
      value: this.value + 1
    }));
  }
}

customElements.define('my-counter', Counter);
```

## Security

Web components often require external scripts. You must relax the Content Security Policy (CSP).

```python
@me.page(
  security_policy=me.SecurityPolicy(
    allowed_script_srcs=["https://cdn.jsdelivr.net"],
    dangerously_disable_trusted_types=True # Often needed for Lit/Firebase
  )
)
```

## Event Handling

Events sent from JS arrive as `me.WebEvent`.

```python
def on_change(e: me.WebEvent):
  state = me.state(State)
  # payload is in e.value
  state.count = e.value["value"]
```

## Tips

- **Validation**: Use Pydantic models to validate `e.value` payloads in Python.
- **Serialization**: Properties passed to JS must be JSON-serializable.
- **Bi-directional**: Python updates properties -> JS re-renders. JS dispatches events -> Python updates state -> Python re-renders -> JS updates properties.
- **Firebase Auth**: A common use case is wrapping Firebase Auth UI. See `mesop.examples` for reference.
