<a name="Component"></a>

## Component
Base class for authoring a vanilla NativeScript component using a friendly syntax.
This class introduces functionality like automatically providing a reference
to its view and automatically binding properties to the component that are passed in
as XML attributes or as `navigationContext` properties.

**Kind**: global class  

* [Component](#Component)
    * _instance_
        * [.view](#Component+view) : <code>ui/View</code>
        * [.bindingContext](#Component+bindingContext) : <code>Observable</code>
        * [.navigationContext](#Component+navigationContext) : <code>Object</code>
        * [.modalContext](#Component+modalContext) : <code>Object</code>
        * [.set(name, value)](#Component+set)
        * [.get(name)](#Component+get) ⇒
        * [.onNavigatingTo(options)](#Component+onNavigatingTo)
        * [.onNavigatedTo(options)](#Component+onNavigatedTo)
        * [.onLoaded(options)](#Component+onLoaded)
        * [.onShownModally(options)](#Component+onShownModally)
        * [.showModal(options)](#Component+showModal) ⇒ <code>Promise</code>
        * [.closeModal(err, data)](#Component+closeModal)
        * [.init(options)](#Component+init)
    * _static_
        * [.isSingleton](#Component.isSingleton) : <code>boolean</code>
        * [.export(exports)](#Component.export)

<a name="Component+view"></a>

### component.view : <code>ui/View</code>
The component's view.

**Kind**: instance property of <code>[Component](#Component)</code>  
<a name="Component+bindingContext"></a>

### component.bindingContext : <code>Observable</code>
The component's unique binding context.

Normally, a NativeScript view implicitly inherits its parent view's `bindingContext` if
its own hasn't been set. However, in order to ensure that each Component instance has its own
context (i.e. so that the context of a Component doesn't collide with that of its parent or
siblings) this class automatically assigns the view its own unique `bindingContext`.

**Kind**: instance property of <code>[Component](#Component)</code>  
<a name="Component+navigationContext"></a>

### component.navigationContext : <code>Object</code>
Contains any navigation context properties passed during the transition.

**Kind**: instance property of <code>[Component](#Component)</code>  
<a name="Component+modalContext"></a>

### component.modalContext : <code>Object</code>
Optional context provided if the component was shown modally.

**Kind**: instance property of <code>[Component](#Component)</code>  
<a name="Component+set"></a>

### component.set(name, value)
Sets a property on the component's binding context.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | property name |
| value |  | property value |

<a name="Component+get"></a>

### component.get(name) ⇒
Gets a property from the component's binding context.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type | Description |
| --- | --- | --- |
| name | <code>string</code> | property name |

<a name="Component+onNavigatingTo"></a>

### component.onNavigatingTo(options)
Hook for the view's `navigationTo` event which automatically sets the component's
`view` property and automatically binds the `navigationContext` properties to the
component instance.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type |
| --- | --- |
| options | <code>Object</code> | 
| options.object | <code>ui/View</code> | 

<a name="Component+onNavigatedTo"></a>

### component.onNavigatedTo(options)
Hook for the view's `navigatedTo` event.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type |
| --- | --- |
| options | <code>Object</code> | 
| options.object | <code>ui/View</code> | 
| options.object.navigationContext | <code>Object</code> | 

<a name="Component+onLoaded"></a>

### component.onLoaded(options)
Hook for the view's `loaded` event which automatically sets the component's `view` property
and binds any properties passed as XML attributes to the component's `bindingContext`. If the no
properties are passed as XML attributes, then the `bindingContext` is not set, allowing the UI
to instead use the parent component's `bindingContext`.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type |
| --- | --- |
| options | <code>Object</code> | 
| options.object | <code>ui/View</code> | 

<a name="Component+onShownModally"></a>

### component.onShownModally(options)
Hook for the view's `shownModally` event which automatically sets the component's
`view` property, binds the `navigationContext` properties to the
component instance and sets its `closeModal` function.

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> |  |
| options.object | <code>ui/View</code> |  |
| options.context |  | Modal context |
| options.closeCallback | <code>function</code> |  |

<a name="Component+showModal"></a>

### component.showModal(options) ⇒ <code>Promise</code>
Launches the given modal on the current page, passing the modal page a Node-style callback to call.

**Kind**: instance method of <code>[Component](#Component)</code>  
**Returns**: <code>Promise</code> - - A promise containing the results passed back by the modal.  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> |  |
| options.modal | <code>string</code> &#124; <code>Page</code> | The path, from the root of the project, to the modal view or the                                               Page instance you which to display as the modal. |
| [options.context] |  | Optional context to pass to to the modal view. |
| [options.fullscreen] | <code>boolean</code> | Optionally specify whether the modal should appear full screen. |

<a name="Component+closeModal"></a>

### component.closeModal(err, data)
If the component was shown modally, this method calls the callback that was provided to `showModal()`.
If it was shown modally using this class's `showModal` method, the callback is a Node-style callback.
If it was not shown modally using this class's `showModal` method, the parameters depend on what is
expected by the code that showed the modal.

**Kind**: instance method of <code>[Component](#Component)</code>  
**Throws**:

- <code>Error</code> - Throws an error if the component wasn't shown modally.


| Param | Type | Description |
| --- | --- | --- |
| err | <code>Error</code> &#124; <code>string</code> &#124; <code>null</code> | The error if an error ocurred, or else `null`. |
| data |  | The result, if there is one. |

<a name="Component+init"></a>

### component.init(options)
A common initialization method invoked by the various lifecycle hooks (e.g. `onLoaded`, `onNavigatingTo`).

**Kind**: instance method of <code>[Component](#Component)</code>  

| Param | Type | Description |
| --- | --- | --- |
| options | <code>Object</code> |  |
| options.object | <code>ui/View</code> |  |
| options.object.navigationContext |  |  |
| options.object[* |  | Any properties passed as custom XML attributes. |

<a name="Component.isSingleton"></a>

### Component.isSingleton : <code>boolean</code>
By default, multiple instances of the component can be created,
and each instance is destroyed upon its view's `unloaded` event. To change this behavior so
that only a single instance of your component is created and is kept alive throughout
the lifetime of your application, override this property to be `true`.

**Kind**: static property of <code>[Component](#Component)</code>  
<a name="Component.export"></a>

### Component.export(exports)
Exports the component's public methods as named exports for a module. This should be called
after the `Component` subclass is defined.

**Kind**: static method of <code>[Component](#Component)</code>  

| Param | Type | Description |
| --- | --- | --- |
| exports | <code>Object</code> | The `exports` variable for the module from which the component's                           methods should be exported. |

**Example**  
```js
class MyComponent extends Component {
    // Extend component methods and use properties
}
MyComponent.export(exports);
```