# numpydoc.el

[![CI](https://github.com/douglasdavis/numpydoc.el/actions/workflows/ci.yml/badge.svg)](https://github.com/douglasdavis/numpydoc.el/actions/workflows/ci.yml)
[![builds.sr.ht status](https://builds.sr.ht/~ddavis/numpydoc.el/commits/.build.yml.svg)](https://builds.sr.ht/~ddavis/numpydoc.el/commits/.build.yml?)

An Emacs Lisp package to automatically insert [NumPy style
docstrings](https://numpydoc.readthedocs.io/en/latest/format.html) for
Python functions.

Calling `numpydoc-generate` will parse the function signature (for the
function corresponding to the current cursor location) and detects
argument names, argument type hints, and return type hints. The
default behavior is to prompt the user (in the minibuffer) for a
(short and long) description of the function, and a description for
each argument and the returned value. If exceptions are detected in
the function body (and `numpydoc-insert-raises-block` is `t`),
exceptions are added to the docstring (with the same prompt behavior
used for function arguments). If the prompt is off
(`numpydoc-prompt-for-input` is `nil`), then some customizable
template text will be inserted into the docstring. If an existing
docstring is detected, you'll be asked if you'd like to delete it and
start fresh.

## Customization

See inside Emacs with <kbd>M-x customize-group RET numpydoc</kbd>

<dl>
  <dt>numpydoc-prompt-for-input</dt>
  <dd>
  If <code>t</code> you will be prompted to enter a short description
  and long description, a description for each function argument, and
  a description for the return (if a return type hint is provided).
  </dd>
  <dt>numpydoc-quote-char</dt>
  <dd>
  Quote character to use (the default is a double quote,
  <code>?\"</code>, used throughout the numpydoc docstring guide and
  the black formatting tool).
  </dd>
  <dt>numpydoc-insert-examples-block</dt>
  <dd>
  If <code>t</code> an Examples block will be added to the docstring.
  </dd>
  <dt>numpydoc-insert-raises-block</dt>
  <dd>
  If <code>t</code> a Raises bock will be added to the docstring if
  exceptions are detected in the function body.
  </dd>
  <dt>numpydoc-template-short</dt>
  <dd>
  Template text that will be used as the short description if
  <code>numpydoc-prompt-for-input</code> is <code>nil</code>.
  </dd>
  <dt>numpydoc-template-long</dt>
  <dd>
  Template text that will be used as the long description if
  <code>numpydoc-prompt-for-input</code> is <code>nil</code>.
  </dd>
  <dt>numpydoc-template-desc</dt>
  <dd>
  Template text that will be used for each function argument
  description if <code>numpydoc-prompt-for-input</code> is
  <code>nil</code>.
  </dd>
</dl>

## Examples

<kbd>M-x numpydoc-generate</kbd> with the default configuration that
will prompt for input in the minibuffer (notice how long text is
automatically paragraph-filled):

<p align="center">
<img src="doc/example.gif" style="border-radius:10px"/>
</p>

Or, <kbd>M-x numpydoc-generate</kbd> with
`numpydoc-prompt-for-input` set to `nil`:

Before:

```python
def plot_histogram(
    x: np.ndarray,
    bins: int = 10,
    range: Optional[Tuple[float, float]] = None,
    weights: Optional[np.ndarray] = None,
    flow: bool = False,
    ax: Optional[plt.Axes] = None,
) -> Tuple[plt.Figure, plt.Axes]:
    pass
```

After:

```python
def plot_histogram(
    x: np.ndarray,
    bins: int = 10,
    range: Optional[Tuple[float, float]] = None,
    weights: Optional[np.ndarray] = None,
    flow: bool = False,
    ax: Optional[plt.Axes] = None,
) -> Tuple[plt.Figure, plt.Axes]:
    """FIXME: Short description.

    FIXME: Long description.

    Parameters
    ----------
    x : np.ndarray
        FIXME: Add docs.
    bins : int
        FIXME: Add docs.
    range : Optional[Tuple[float, float]]
        FIXME: Add docs.
    weights : Optional[np.ndarray]
        FIXME: Add docs.
    flow : bool
        FIXME: Add docs.
    ax : plt.Axes
        FIXME: Add docs.

    Returns
    -------
    Tuple[plt.Figure, plt.Axes]
        FIXME: Add docs.

    Examples
    --------
    FIXME: Add docs.

    """
    pass
```

## Similar packages

- [sphinx-doc.el](https://github.com/naiquevin/sphinx-doc.el): Inserts
  sphinx-compatible docstrings (does not offer customizations or
  automatically formatted insertions from minibuffer prompt).
