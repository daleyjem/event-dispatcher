# event-dispatcher

A generic vehicle for dispatching and listening to events.

## Objects

### EventDispatcher

#### addEventListener(type:string, callback:any)

#### removeEventListener(type:string, callback:any)

#### dispatchEvent(type:string)

### DispatchableEvent

## Usage

### Extending

```
import { EventDispatcher, DispatchableEvent } from 'event-dispatcher';

class SomeClassOrService extends EventDispatcher {
	public static MY_EVENT:string = 'my_event';

    construct(){
        super();
        
        setTimeout( () => {
        	this.dispatchEvent( new DispatchableEvent( SomeClassOrService.MY_EVENT ));
        }, 5000);
    }
}
```

### Consuming

```
import DispatchableEvent from 'event-dispatcher';
import SomeClassOrService from './some-class-or-service';

class SomeOtherClassOrService {
    constructor(
        private someClassOrService:SomeClassOrService;
    ){
        this.someClassOrService.addEventListener( SomeClassOrService.MY_EVENT, this.onMyEvent.bind( this ));
    }
    
    private onMyEvent(){
        console.log( 'MY_EVENT fired' );
    	this.someClassOrService.removeEventListener( SomeClassOrService.MY_EVENT, this.onMyEvent.bind( this ));
    }
}
```