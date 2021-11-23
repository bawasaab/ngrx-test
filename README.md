# ngrx-test

# NGRX

# STEP-1

import reducer from reducer file
create store in app module key as count and value as counterReducer forRoot({
    count: counterReducer
})
=======================================================================

# STEP-2
Goto reducer file and import actions from action file
import { increment, decrement, reset } from './counter.actions';
=======================================================================

# STEP-3
in actions file create actions using createAction method and export actions 
import { createAction } from '@ngrx/store';

export const increment = createAction('[Counter Component] Increment');
export const decrement = createAction('[Counter Component] Decrement');
export const reset = createAction('[Counter Component] Reset');
=======================================================================

# STEP-4

in reducer file create reducer using createReducer method and export reducer 
import { Action, createReducer, on } from '@ngrx/store';
import { increment, decrement, reset } from './counter.actions';

export const initialState = 0;

const _counterReducer = createReducer(
  initialState,
  on(increment, (state) => state + 1),
  on(decrement, (state) => state - 1),
  on(reset, (state) => 0)
);

export function counterReducer(state: any, action: Action) {
  return _counterReducer(state, action);
}
=======================================================================

# STEP-5

in reducer file and intialize the intial state 
export const initialState = 0;
=======================================================================

# STEP-6

import Store, Observable, actions from STEP-3 in the component file
import { Store } from '@ngrx/store';
import { Observable } from 'rxjs';
import { increment, decrement, reset } from '../store/counter.actions';
=======================================================================

# STEP-7

instantiate store with key defined in STEP-1 
constructor(private store: Store<{ count: number }>) {
		this.count$ = store.select('count');
}
=======================================================================

# STEP-8

create a variable as observable in component
count$: Observable<number>;
=======================================================================

  
# STEP-9
	
inside  constructor select store using the key defined in the app module StoreModule.forRoot
this.count$ = store.select('count');
=======================================================================

# STEP-10 FINAL STEP
	
now in your component, inside methods dispatch the actions 
import { Component, OnInit } from '@angular/core';

import { Store } from '@ngrx/store';
import { Observable } from 'rxjs';
import { increment, decrement, reset } from '../store/counter.actions';

@Component({
  selector: 'app-my-counter',
  templateUrl: './my-counter.component.html',
  styleUrls: ['./my-counter.component.css']
})
export class MyCounterComponent implements OnInit {

	count$: Observable<number>;
	
	constructor(private store: Store<{ count: number }>) {
		this.count$ = store.select('count');
	}

  ngOnInit(): void {
  }  
 
  increment() {
    this.store.dispatch(increment());
  }
 
  decrement() {
    this.store.dispatch(decrement());
  }
 
  reset() {
    this.store.dispatch(reset());
  }
}
=======================================================================

# STEP-11 HTML
	
<button (click)="increment()">Increment</button>

<div>Current Count: {{ count$ | async }}</div>

<button (click)="decrement()">Decrement</button>

<button (click)="reset()">Reset Counter</button>
=======================================================================
