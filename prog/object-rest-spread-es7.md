Pulled this today https://github.com/anorudes/redux-easy-boilerplate
```
  case 'DELETE_ITEM':
    return {
      ...state,
      items: [
        ...state.items.slice(0, action.index),
        ...state.items.slice(+action.index + 1),
      ],
    };
```

In some reducer code I saw something like this. Redux revolves around immutability so I knew it was cloning the state and removing from 1 from items (also cloned).


wtf is '...' how does that work. Look at compiled es5.
    var _extends = Object.assign || function (target) { for (var i = 1; i < arguments.length; i++) { var source = arguments[i]; for (var key in source) { if (Object.prototype.hasOwnProperty.call(source, key)) { target[key] = source[key]; } } } return target; };
    function _toConsumableArray(arr) { if (Array.isArray(arr)) { for (var i = 0, arr2 = Array(arr.length); i < arr.length; i++) arr2[i] = arr[i]; return arr2; } else { return Array.from(arr); } }

    case 'DELETE_ITEM':
      return _extends({}, state, {
        items: [].concat(_toConsumableArray(state.items.slice(0, action.index)), _toConsumableArray(state.items.slice(+action.index + 1)))
      });

wtf is ... called? splat? pre-splat? google help me.

nope

https://github.com/sebmarkbage/ecmascript-rest-spread

return {
  newState = Object.assign({}, state)
  newState.items = state.items.slice()
  newState.items.splice(action.index, 1)
  return newState
}
? shim Object.Assign?