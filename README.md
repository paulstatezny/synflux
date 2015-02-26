# synflux
My own personal Flux implementation

# How to use it

Like this:

```JS
var Synflux = require('synflux');

// Make a store
var store = Synflux.createStore({
    initialize : function()
    {
        this.data = {};

        this.bindActions('SET_DATA', 'onSetData');
    },

    onSetData : function(data)
    {
        this.data = data;
    },

    getData : function()
    {
        return this.data;
    }
});

// Make an action creator
var action = {
    setData : function(data)
    {
        this.dispatch('SET_DATA', data);
    }
};

// Register with the flux object
var flux = Synflux.Flux({Data : store}, {Data : action});
```

And then, here's how you'd use it in your React components:

```JS
var SomeReactComponent = React.createClass({
    mixins : [
        SynFlux.StoreWatchMixin('Data'),
        SynFlux.FluxMixin
    ],

    // ...

    getStateFromFlux : function()
    {
        return {
            data : this.getFlux().store('Data').getData()
        };
    },

    onUserChangesData : function(data)
    {
        this.getFlux().actions.Data.setData(data);
    },

    render : function()
    {
        // Render stuff
    }
});
```
