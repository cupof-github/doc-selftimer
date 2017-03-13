# self-timer.js <small>1.4.4</small>

![logo](_assets/img/logo.png)

Date based callback runner library for Javascript

## About

?> The **self-timer.js** is a light-weight callback runner library for javascript. You may let your callback to run at the timing when you want to execute.

<!-- <h2 id="installation"><i class="fa fa-paperclip"></i> Installation</h2> -->
## Installation

```bash
# npm
npm install self-timer --save
```

```html
<!-- cdn  -->

<!-- callback  -->
<script src="https://unpkg.com/self-timer/dist/selftimer.min.js"></script>
<!-- promise  -->
<script src="https://unpkg.com/self-timer/dist/selftimer-promise.min.js"></script>
<!-- promise but including polyfill  -->
<script src="https://unpkg.com/self-timer/dist/selftimer-promise-polyfill.min.js"></script>
```

## Usage

The **self-timer.js** have 2 types and 3 differences of files. You may choose them in right scene.

- callback style [ `selftimer.js` ( **.min.js: 7KB** ) ]
- promise style [ `selftimer-promise.js` ( **.min.js: 7KB )** ]
- promise style with Polyfill [ `selftimer-promise-polyfill.js` - **(.min.js: 10KB)** ]

!> **Note: selftimer-promise-polyfill is including [taylorhakes/promise-polyfill](https://github.com/taylorhakes/promise-polyfill). Very thanks!**

#### Callback style.

> This is callback style, writing code with basic callback style

```javascript
// selftimer.min.js
var st = new SelfTimer(new Date());

st.on()
    .Selects(["Mon", "Wed", "Fri"], function() {
      // callback
      console.log("runs on Monday, Wednesday, Friday!");
    });
```

#### Promise style.

> This is Promise style so, you may use promise method. like, 'then()', 'catch'

```javascript
// selftimer-promise-plyfill.min.js || selftimer-promise.min.js
var st = new SelfTimer(new Date());

st.on()
  .Selects(["Mon", "Wed", "Fri"])
    .then(function(){
      // callback
      console.log("runs on Monday, Wednesday and Friday!");
    });

// or if attach "true" param in group ( * on() ), you can use "catch()" method
st.on(true)
  .Selects(["Mon", "Wed", "Fri"])
    .then(function(){
      // callback
      console.log("runs on Monday, Wednesday and Friday!");
      })
    .catch(function(){
      // callback
      console.log("runs on UNLESS Monday, Wednesday and Friday!");
      });
```
Of course, self-timer.js is applied to the UMD( Universal Module Definition) thus, you may use it on Browser, ES6 and commonJS scenes.

**browser**
```html
<!-- read self-timer.js in your browser -->
<script src="./self-timer/dist/selftimer.min.js"></script>
<!-- if you use promise -->
<!-- <script src="./self-timer/dist/selftimer-promise-polyfill.min.js"></script> -->

<script>
// initialize
var st = new SelfTimer(new Date());

st.on()
    .Selects(["Mon", "Wed", "Fri"], function() {
      // callback
      console.log("runs on Monday, Wednesday, Friday!");
    });
</script>
```
**ES6**
```javascript
// es6 style. like babel, webpack and so.
import SelfTimer from 'self-timer';

/* if you use promise */
// import SelfTimer from 'self-timer/dist/selftimer-promise'

// initialize
const st = new SelfTimer(new Date());

st.on().Sunday(() => {
 console.log("run on Sunday");
});
```

**CommonJS**
```javascript
// CommonJS style. * node.js
const SelfTimer = require('self-timer');

/* if you use promise */
// const SelfTimer = require('self-timer/dist/selftimer-promise');

// initialize
const st = new SelfTimer(new Date());

st.on().Monday(() => {
 console.log("run on Monday");
});
```

## Sunday( task ) ... Saturday( task )
> This  methods  are return callback, when you want to run on days of the week.  ( * Sunday to Saturday )

- group : `.on()`
- argument : `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

/* -- Available methods --
  Sunday(), Monday(), Tuesday(), Wednesday(),
  Thursday(), Friday(), Saturday()
*/

// Sunday()
st.on().Sunday(function() {
  // callback
  console.log("this run when Sunday!")
});

....

// with non-callback
if( st.on().Tuesday() ) {
  // callback
  console.log("this run when Tuesday");
}

if( ! st.on().Tuesday() ) {
  // callback
  console.log("this run when not on Tuesday");
}

```
**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new selfTimer(new Date());

/* -- Available methods --
  Sunday(), Monday(), Tuesday(), Wednesday(),
  Thursday(), Friday(), Saturday()
*/

// Sunday()
st.on()
    .Sunday()
      .then(function(){
        // callback
      });

// use 'catch' method
st.on(true)
    .Friday()
      .then(function(){
          // calback
        })
      .catch(function(){
          // this run when not on Friday
      });
```

## Weekdays( task )
> ``Weekdays`` method return callback, when **weekdays** ( Monday to Friday ).

- group : `.on()`
- argument : `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Weekdays() * run Monday to Friday
st.on().Weekdays(function() {
  // callback
  console.log("running on Monday to Friday!");
});

// non-callback
if( st.on().Weekdays() )
{
  // callback
  console.log("running on Monday to Friday!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Weekdays() * run Monday to Friday
st.on()
    .Weekdays()
      .then(function(){
        // callback
        console.log("running on Monday to Friday!");
      });

// use 'catch' case
st.on(true)
    .Weekdays()
      .then(function(){
        // callback
        })
      .catch(function(){
        // callback
      });
```

## Weekend( task )

> `Weekend` method return callback, when **weekend** ( Sunday and Saturday ).

- group : `.on()`
- argument : `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Weekend() * run Sunday and Saturday
st.on().Weekend(function() {
  // callback
  console.log("do something on weekend!");
});

// non-callback
if( st.on().Weekend() )
{
  //callback
  console.log("do something on weekend!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Weekend() * run Sunday and Saturday
st.on()
    .Weekend()
      .then(function(){
        // callback
        console.log("do something on weekend!");
      });

// use 'catch' method
st.on(true)
    .Weekend()
      .then(function(){
        // callback
        })
      .catch(function(){
        // callback
      });
```

## Selects( daysOfTheWeek, task )

> `Selects` method return callback, when you want to run **days of the week** ( * Sunday to Saturday ) you selected.

- group : `.on()`
- argument : `daysOfTheWeek` [ Array ] * [ Sun, Mon, Tue, Wed, Thu, Fri, Sat ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Selects() * run Monday, Wednesday, Friday.
st.on().Selects(["Mon", "Wed", "Fri"], function() {
  // callback
  console.log("run on Monday, Wednesday and Friday!");
});

// non-callback
if( st.on().Selects(["Tue", "Thu", "Sat", "Sun"]) )
{
  // callback
  console.log("run on Tuesday, Thursday, Saturday and Sunday!");
}

if( ! st.on().Selects(["Tue", "Thu", "Sat", "Sun"]) )
{
  // callback
  console.log(" NOT run on Tuesday, Thursday, Saturday and Sunday!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Selects() * run Monday, Wednesday, Friday.
st.on()
    .Selects(["Mon", "Wed", "Fri"])
      .then(function(){
        // callback
        console.log("run on Tuesday, Thursday, Saturday and Sunday!");
      });

// use 'catch' method
st.on(true)
    .Selects(["Mon", "Wed", "Fri"])
      .then(function(){
        // callback
        console.log("run on Tuesday, Thursday, Saturday and Sunday!");
        })
      .catch(function(){
        //callback
      });
```

## Annual( date, task )

> `Annual` method return callback when you want to run **months of days**

- group : `.on()`
- argument : `date` [ String ] * MM-dd , `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Annual() * Nov 2.
st.on().Annual('11-2', function() {
  // callback
  console.log("do something on Nov 2!");
});

// non-callback
if( st.on().Annual('12-25') )
{
  // callback
  console.log("do somting on December 25!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Annual() * Nov 2.
st.on()
    .Annual('11-2')
      .then(function(){
        // callback
        console.log("run on Nov 2!");
      });

// use 'catch' method
st.on(true)
    .Annual('11-2')
      .then(function(){
        // callback
          console.log("run on Nov 2!");
        })
      .catch(function(){
        // callback
      });
```

## DatesBetween( from, to, task )

> `DatesBetween` method return callback, when you want to run **between two dates.**

- group : `.on()`
- argument : `from` [ String ] *YYYY-MM-DD* , `to` [ String ] *YYYY-MM-DD* , `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// DatesBetween() * Nov 2, 2016 to Nov 17, 2016
st.on().DatesBetween('2016-11-2', '2016-11-17', function() {
  // callback
  console.log("do something on Nov 2, 2016 to Nov 17, 2016 !");
});

// non-callback Dec 24, 2016 to Dec 26, 2016
if( st.on().DatesBetween('2016-12-24', '2016-12-26') )
{
  // callback
  console.log("do something on December 24, 2016 to December 26, 2016!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// DatesBetween() * Nov 2, 2016 to Nov 17, 2016
st.on()
    .DatesBetween('2016-11-2', '2016-11-17')
      .then(function() {
        // callback
        console.log("do something on Nov 2, 2016 to Nov 17, 2016 !");
      });

// use 'catch' method
st.on(true)
    .DatesBetween('2016-11-2', '2016-11-17')
      .then(function() {
        // callback
        console.log("do something on Nov 2, 2016 to Nov 17, 2016 !");
        })
      .catch(function(){
        // callback
      });
```

## DatesContain( dates, task )

> `DatesContain` method return callback when you want to run date.

> It is similar to `Annual` method, but this method has supported `multiple dates`.

- group : `.on()`
- argument : `dates` [ Array ] *yyyy-mm-dd* , `task` [ Function ]
- return : `Function` || `Bool`
- NOTE: **available since v1.1.0**

** callback **

```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date('2017-03-01'));

// DatesContain
st.on().DatesContain(['2017-03-01', '2017-04-02'], function() {
  console.log(" run on 'March 1, 2017' and 'April 2', 2017");
});
```

** promise **

``` javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// DatesContain
st.on()
    .DatesContain(['2017-03-01', '2017-04-02'])
      .then(function() {
          console.log("この処理は '2017年3月1日' と '2017年4月2日' に実行されます ");
        });

// use 'catch' method
st.on()
   .DatesContain(['2017-03-01', '2017-04-02'])
    .then(function() {
      console.log("この処理は '2017年3月1日' と '2017年4月2日' に実行されます ");
      })
    .catch(function(){
      // callback
    });


```

### Between( from, to, task )

> `Between` method return callback, **between times start to end**.

- group : `.at()`
- argument : `from` [ String ] *hh:mm* ( am || pm ), `to` [ String ] *hh:mm* ( am || pm ), `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Between() usage
st.at().Between('9:00 am', '5:30 pm', function() {
  console.log('we are opening!');
});
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Between() usage
st.at()
    .Between('9:00 am', '5:30 pm')
      .then(function() {
        console.log('we are opening!');
      });

// use 'catch' method
st.at(true)
    .Between('9:00 am', '5:30 pm')
      .then(function() {
          console.log('we are opening!');
        })
      .catch(function(){
        // callback
      });
```

**example**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this example run on Monday to Friday at 9 am to 5:30 pm.
st.on().Weekdays(function() {

  st.at().Between('9:00 am', '5:30 pm', function() {
    // callback
    console.log('we are opening!');
  });

});
```

## Unless( from, to, task )

> `Unless` method return callback, **exclude times from start to end**.

- group : `.at()`
- argument : `from` [ String ] * hh:mm ( am || pm ), `to` [ String ] * hh:mm ( am || pm ), `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Unless() usage
st.at().Unless('9:00 am', '5:30 pm', function() {
  console.log('this method run unless 9:00 am to 5:30 pm.');
});
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Unless() usage
st.at()
    .Unless('9:00 am', '5:30 pm')
      .then(function() {
          // callback
          console.log('this method run unless 9:00 am to 5:30 pm.');
        });

// use 'catch' method
st.at(true)
    .Unless('9:00 am', '5:30 pm')
      .then(function() {
          // callback
          // this method run unless 9:00 am to 5:30 pm.
          console.log('we are closing.');
        })
      .catch(function(){
          // callback
          console.log('we are opening!')
      });
```

**example**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this method run on Monday to Friday at 9 am to 5:30 pm.
st.on().Weekdays(function() {

  st.at().Unless('9:00 am', '5:30 pm', function() {
    // callback
    console.log('we are closing!');
  });

});
```

## Hour( hour, task )

> `Hour` method return callback, when you want to run **hour of time**.

- group : `.at()`
- argument : `hour` [ Integer ] * 0 - 23, `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Hour().
st.at().Hour(20, function() {
  // callback
  console.log("do something at 8 pm!");
});

// non-callback
if( st.at().Hour(8) )
{
  // callback
  console.log("run at 8 am!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Hour().
st.at()
    .Hour(20)
      .then(function() {
        // callback
        console.log("do something at 8 pm!");
      });

// use 'catch' method
st.at(true)
    .Hour(20)
      .then(function() {
          // callback
          console.log("run at 8 pm!");
        })
      .catch(function(){
          // callback
      });
```

## HoursBetween( from, to, task )

> `HoursBetween` method return callback, **between hour of times start to end**.

- group : `.at()`
- argument : `from` [ Integer ], `to` [ Integer ] ,`task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this method run 1 pm to 3 pm
st.at().HoursBetween(13, 15, function() {
  // callback
  console.log('we are temporally closing!');
});
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// this method run 1 pm to 3 pm
st.at()
    .HoursBetween(13, 15);
      .then(function() {
        // callback
        console.log('we are temporally closing!');
      });

// use 'catch' method
st.at(true)
    .HoursBetween(13, 15);
      .then(function() {
          // callback
          console.log('we are temporally closing!');
        })
      .catch(function(){
        // callback
      });
```

**example**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this method run on Monday to Friday at 1 pm to 3 pm.
st.on().Weekdays(function() {
  // this method run 1 pm to 3 pm
  st.at().HoursBetween(13, 15, function() {
    // callback
    console.log('we are temporally closing!');
  });

});
```

## HourSelects( hours, task )

> `HourSelects` method return callback, **when mataching an hour your selected.**

> *while 1pm, 3pm and so.

- group : `.at()`
- argument : `hours` [ Array ] ( 0 - 23 ) ,`task` [ Function ]
- return : `Function` || `Bool`
- NOTE: **available since v1.2.0**

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this method to run 1:00 ~ 1:59 pm AND 3:00 ~ 3:59 pm
st.at().HourSelects([13, 15], function() {
  // callback
  console.log("this method to run, while 1 pm and 3 pm");
});
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// HourSelects()
st.at()
    .HourSelects([13, 15]);
      .then(function() {
        // callback
        console.log("this method to run, while 1 pm and 3 pm");
      });

// use 'catch' method
st.at(true)
    .HourSelects([13, 15]);
      .then(function() {
          // callback
          console.log("this method to run, while 1 pm and 3 pm");
        })
      .catch(function(){
        // callback
      });
```

## Day( Day, task )

> `Day` method return callback, when you want to run **day in month**.

- group : `.in()`
- argument : `Day` [ Integer ] * 1 - 31, `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Day() * run in 10th.
st.in().Day(10, function() {
  // callback
  console.log("run at 10th monthly !");
});

// non-callback
if( st.in().Day(10) )
{
  // callback
  console.log("run at 10th monthly !");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Day() * run in 10th.
st.on()
    .Day(10)
      .then(function() {
        // callback
        console.log("run at 10th monthly !");
      });

// use 'catch' method
st.on(true)
    .Day(10)
      .then(function() {
          // callback
          console.log("run at 10th monthly !");
        })
      .catch(function(){
        // callback
      });
```

## Days( days, task )

> `Days` method return callback, when you want to run multiple days you selected.　( * exp 3th, 7th, 14th ... etc in Month )

- group : `.in()`
- argument : `days` [ Array ] * exp [1, 3, 7, 31], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Days()
st.in().Days([3, 10, 13, 23], function() {
  // callback
  console.log("run on 3th, 10th, 13th, 23th in month");
});

// non-callback
if( st.in().Days([3, 10, 13, 23]) )
{
  // callback
  console.log("run on 3th, 10th, 13th, 23th in month");
}

```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Days()
st.in()
    .Days([3, 10, 13, 23])
      .then(function() {
        // callback
        console.log("run on 3th, 10th, 13th, 23th in month");
      });

// use 'catch' method
st.in(true)
    .Days([3, 10, 13, 23])
      .then(function() {
          // callback
          console.log("run on 3th, 10th, 13th, 23th in month");
        })
      .catch(function(){
        // callback
      });
```


## DaysBetween( from, to, task )

> `DaysBetween` method return callback, **between times start to end**.

- group : `.in()`
- argument : `from` [ Integer ] * up to 31, `to` [ Integer ] * up to 31, `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// DaysBetween() usage
st.in().DaysBetween(10, 16, function() {
  // callback
  console.log('this method run between 10th to 16th in month !');
});

if( st.in().DaysBetween(10, 16) )
{
  // callback
  console.log('this method run between 10th to 16th in month !');
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// DaysBetween() usage
st.in()
    .DaysBetween(10, 16)
      .then(function() {
        console.log('this method run between 10th to 16th in month !');
      });

// use 'catch' method
st.in(true)
    .DaysBetween(10, 16)
      .then(function() {
          console.log('this method run between 10th to 16th in month !');
        })
      .catch(function(){
          // callback
      });
```

## Month( month, task )

> `Month` method return callback, when you want to run **in Months** ( * January to December ).

- group : `.in()`
- argument : `month` [ Integer ] * 1 - 12, `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Month() * run Month
st.in().Month(12, function() {
  // callback
  console.log("run during December!");
});

// non-callback
if( st.in().Month(12) )
{
  // callback
  console.log("run during December!");
}

```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Month()
st.in()
    .Month(12)
      .then(function() {
        // callback
        console.log("run during December!");
      });

// use 'catch' method
st.in(true)
    .Month(12)
      .then(function() {
        // callback
        console.log("run during December!");
        })
      .catch(function(){
        // callback
      });

```

## MonthSelects( months, task )

> `MonthSelects` method return callback, when you want run **months**.

- group : `.in()`
- argument : `months` [ Array ] * exp: [6, 7, 8], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// MonthSelects() usage
st.in().MonthSelects([7, 8], function() {
  console.log('this method run in July to August!');
});

// non-callback
if( st.in().MonthSelects([7, 8]) )
{
  // callback
  console.log('this method run in July to August!');
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// MonthSelects() usage
st.in()
    .MonthSelects([7, 8])
      .then(function() {
        // callback
        console.log('this method run in July to August!');
      });

// use 'catch' method
st.in()
    .MonthSelects([7, 8])
      .then(function() {
          // callback
          console.log('this method run in July to August!');
        })
      .catch(function(){
        // callback
      });
```

**example**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// this method run in July to August on Saturday and Sunday.
st.in().MonthSelects([7, 8], function() {
  // callback
  st.on().Weekend(function(){
    // callback
    console.log('We have "Summer Sales" July to August on Weekend ! ')
  });

});
```

## Year( Year, task )

> `Year` method return callback, when you want to run `during Year` ( * 2016, 2017 .. etc ).

- group : `.in()`
- argument : `year` [ Integer ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Year()
st.in().Year(2016, function() {
  // callback
  console.log("this method run, during years of 2016!");
});

// in() method is supported method chaining * if attached 'true' inside in() (Only callback)
st.in(true)
  .Year(2016)
  .MonthSelects([7, 8], function(){
      console.log("this method run, in July and August, 2016!");
  });

// non-callback
if( st.in().Year(2016) )
{
  // callback
  console.log("this method run, during years of 2016!");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Year()
st.in()
    .Year(2016)
    .then(function() {
      // callback
      console.log("this method run, during years of 2016!");
    });

// use 'catch' method
st.in(true)
    .Year(2016)
      .then(function() {
          // callback
          console.log("this method run, during years of 2016!");
        })
      .catch(function(){
          // callback
        });
```

**example**
```javascript
/* use selftimer-promise.js with ES6 syntax */

// initialize
var st = new SelfTimer(new Date());

// this method run on Saturday, November in 2016.
st.in().Year(2016).then(() => {

    // November
    st.in().Month(11).then(() => {

        // Saturday
        st.on(true)
            .Saturday()
              .then(() => {
                  // callback
                  console.log("it's Saturday!");
                })
              .catch(() => {
                  // callback
                  console.log("it's not Saturday!");
              });

    });

});
```

## True( condition, task )

> `True` method return callback, **if condition is true**.

- group : `.is()`
- argument : `condition` [ Bool ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// exp: check cookie exist with js-cookie
function checkExample(param) {
  return Cookies.get(param) !== undefined
                                ? true
                                : false;
}

// initialize
var st = new SelfTimer(new Date());

// True() * run if true.
st.is().True(checkExample('yourParam'), function() {
  // callback
  // extend time for cookie expiration
  Cookies.set('yourParam', 'someValue', { expires: 7 });
});

// non-callback
if( st.is().True(checkExample('yourParam')) )
{
  // callback
  // extend time for cookie expiration
  Cookies.set('yourParam', 'someValue', { expires: 7 });
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// exp: check cookie exist with js-cookie
function checkExample(param) {
  return Cookies.get(param) !== undefined
                            ? true
                            : false;
}

// initialize
var st = new SelfTimer(new Date());

// True() * run if true
st.on()
    .True(checkExample('yourParam'))
      .then(function() {
        // callback
        Cookies.set('yourParam', 'someValue', { expires: 7 });
      });

// with 'catch' method
st.on(true)
    .True(checkExample('yourParam'))
      .then(function() {
          // callback
          Cookies.set('yourParam', 'someValue', { expires: 7 });
        })
      .catch(function(){
          // callback
      });
```

## False( condition, task )

> `False` method return callback, **if condition is false**

- group : `.is()`
- argument : `condition` [ Bool ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// exp: check cookie exist with js-cookie
function checkExample(param) {
  return Cookies.get(param) !== undefined
                        ? true
                        : false;
}

// initialize
var st = new SelfTimer(new Date());

// True() * run if false.
st.is().False(checkExample('yourParam'), function() {
// callback
// create cookie
Cookies.set('yourParam', 'someValue', { expires: 7 });
});

// non-callback
if( st.is().False(checkExample('yourParam')) )
{
// callback
// create cookie
Cookies.set('yourParam', 'someValue', { expires: 7 });
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// exp: check cookie exist with js-cookie
function checkExample(param) {
  return Cookies.get(param) !== undefined
                        ? true
                        : false;
}

// initialize
var st = new SelfTimer(new Date());

// False() * run if condition is false
st.on()
    .False(checkExample('yourParam'))
      .then(function() {
        // callback
        Cookies.set('yourParam', 'someValue', { expires: 7 });
      });

// with 'catch' method
st.on(true)
    .False(checkExample('yourParam'))
      .then(function() {
        // callback
        Cookies.set('yourParam', 'someValue', { expires: 7 });
      })
      .catch(function(){
        // callback
      });
```

## Language( Language, task ) * Web-Browser only

> `Language` method return callback, **when matching user-browser-language to language-string in argument**. ( * exp: 'en-au', 'en-us', 'fr-ch', 'fr-ca' ... etc )

[Ref: Language-code-reference (Microsoft)](https://msdn.microsoft.com/en-us/library/ms533052?v=vs.85.aspx)

- group : `.is()`
- argument : `language` [ String ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Language()
st.is().Language('en-us', function() {
  // callback
  console.log("this method run if user-language is 'en-us'");
});

// non-callback
if( st.is().Language('en-us') )
{
  // callback
  console.log("this method run if user-language is 'en-us'");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Language()
st.is()
    .Language('en-us')
    .then(function() {
        // callback
        console.log("this method run if user-language is 'en-us'");
      });

// use 'catch' method
st.is(true)
    .Language('en-us')
      .then(function() {
          // callback
          console.log("this method run if user-language is 'en-us'");
        })
      .catch(function(){
          // callback
      });
```

## Lang( language, task ) * Web-Browser only

> `Lang` method return callback, **when matching user-browser-langage to language-string in argument**.

> ( * exp: 'en', 'fr', 'de', 'zh', 'ja')


> This is similar method to `Language`. but, this is **sliced string to two characters** (* 'en-us' -> 'en' || 'fr-ch' -> 'fr'　).

[Ref: Language-code-reference (Microsoft)](https://msdn.microsoft.com/en-us/library/ms533052?v=vs.85.aspx)


- group : `.is()`
- argument : `language` [ String ], `task` [ Function ]
- return : `Function` || `Bool`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// Lang()
st.is().Lang('en', function() {
  // callback
  console.log("this method run if user-language is 'english'");
});

// non-callback
if( st.is().Language('en') )
{
  // callback
  console.log("this method run if user-language is 'english'");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// Lang()
st.is()
    .Lang('en')
      .then(function() {
        // callback
        console.log("this method run when user-language is 'english'");
      });

// with 'catch' method
st.is(true)
    .Lang('en')
      .then(function() {
          // callback
          console.log("this method run when user-language is 'english'");
        })
      .catch(function(){
        // callback
      });
```

## LanguageSelects( languages, task ) * Web-Browser only

> `LanguageSelects` method return callback, when matching user-browser-language to language-string in argument. ( * enable multiple languages )

> ( * exp: 'en-au', 'en-us', 'fr-ch', 'fr-ca' ... etc )

> *available `LanguageExcepts` method. it's completely oppsite process to `LanguageSelects`

[Ref: Language-code-reference (Microsoft)](https://msdn.microsoft.com/en-us/library/ms533052?v=vs.85.aspx)


- group : `.is()`
- argument : `languages` [ Array ], `task` [ Function ]
- return : `Function | Bool`
- NOTE: **added since v1.4.0**

**callback**
```javascript
/* selftimer.js */
var st = new SelfTimer(new Date());

// LanguageSelects()
st.is()
  .LanguageSelects(['en-us', 'en-ca'], function() {
    // callback
    console.log("run, if 'en-us or en-ca' in user-browser-language ");
  });

// non-callback
if( st.is().LanguageSelects(['en-us', 'en-ca']) )
{
  // callback
  console.log("run, if 'en-us or en-ca' in user-browser-language ");

}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

var st = new SelfTimer(new Date());

// LanguageSelects()
st.is()
  .LanguageSelects(['en-us', 'en-ca'])
    .then(function() {
      // callback
      console.log("run, if 'en-us or en-ca' in user-browser-language ");
    });

// with catch method
st.is(true)
  .LanguageSelects(['en-us', 'en-ca'])
    .then(function() {
      // resolve method
      console.log("run, if 'en-us or en-ca' in user-browser-language ");
    })
    .catch(function() {
      // reject method
      console.log("run, if not 'en-us or en-ca' in user-browser-language ");
    })
```

## LangSelects( lang, task ) * Web-Browser only

> `LangSelects` method return callback, when matching user-browser-langage to language-string in argument. ( exp: 'en', 'fr', 'de', 'zh', 'ja')

> This is similar method to `LanguageSelects`. but, this is sliced string to two characters ( 'en-us' -> 'en' || 'fr-ch' -> 'fr'　).

> *available `LangExcepts` method. it's completely oppsite process to `LangSelects`

[Ref: Ref: Language-code-reference (Microsoft)](https://msdn.microsoft.com/en-us/library/ms533052?v=vs.85.aspx)

- group : `.is()`
- argument : `lang` [ Array ], `task` [ Function ]
- return : `Function`
- NOTE: **added since v1.4.0**

**callback**
```javascript
/* selftimer.js */

var st = new SelfTimer();

// LangSelects()
st.is()
  .LangSelects(['en', 'fr', 'es'], function() {
    // callback
    console.log("run if user-browser-language is `english or french or español`");
  });

// with non-callback
if ( st.is().LangSelects(['en', 'fr', 'es']) ) {
    // callback
    console.log("run if user-browser-language is `english or french or español`");
}
```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

var st = new SelfTimer(new Date());

st.is()
  .LangSelects(['en', 'fr', 'es'])
    .then(function(){
      // resolve
      console.log("run if user-browser-language is `english or french or español`");
    });

// use catch method
st.is(true)
  LangSelects(['en', 'fr', 'es'])
    .then(function(){
      // resolve
    console.log("run if user-browser-language is `english or french or español`");
    })
    .catch(function(){
      // reject
      console.log("run if not user-browser-language is `english or french or español`");
    });

```

## After( type, num, task)

> `After` method return callback, after a time `( second or minute )` you specified.

- group : `.timer()`
- argument : `type` [ String ], `num` [ Integer ], `task` [ Function || Object ]
- return : `Function`
- NOTE: **added since v1.3.0**

> **available formats for a `type` of argument**

> **second** : `s`, `sec`, `second`, `seconds`

> **minute** : `m`, `min`, `minute`, `minutes`

**callback**
```javascript
/* selftimer.js */

// initialize
var st = new SelfTimer(new Date());

// after 3 seconds
st.timer()
  .After("sec", 3, function() {
    console.log("run, after 3 seconds");
  });

// case of including immediate function
st.timer()
  .After("min", 2, {
    before: function() {
      console.log("run immediately");
    },
    after: function() {
      console.log("run, after 2 minutes");
    }
  });

```

**promise**
```javascript
/* selftimer-promise-plyfill.js || selftimer-promise.js */

// initialize
var st = new SelfTimer(new Date());

// after 3 seconds
st.timer()
  .After("sec", 3)
    .then(function() {
      console.log("run, after 3 seconds");
    });

// case of including immediate function
st.timer()
  .After("min", 2, {
    before: function() {
      console.log("run immediately");
    }
  })
  .then(function() {
    console.log("run, after 2 minutes");
  });
```
