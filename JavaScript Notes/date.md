### GMT kya hai?

**GMT = Greenwich Mean Time**  
Ye ek **time standard** hai jo London ke paas ek jagah **Greenwich Observatory** se nikalta hai.

- Basically, ye earth ki rotation aur Greenwich meridian (0° longitude) k hisaab se banaya gaya tha.

- GMT pehle duniya ka **official reference time** tha, per abh iski jaga UTC use hota hey.

## What is UTC?

It stands for Coordinated Universal Time. Yeah aik universal clock ki traha jo apko duniya mey kahi bhi app ho aik hi wakt dhikati hey. It's used as a reference point or a starting point  to calculate the time, for a specific region or country.

**Why UTC?**

- Har mulk apna local waqt rakh sakta hai (jaise Pakistan Standard Time = UTC +5)

- Lekin international level pe confusion na ho (flights, internet servers, trading, GPS, programming) is liye sab UTC ko base maan k local time calculate karte hain.

### What is ISO 8601?

It’s an **international standard** for representing **date and time** so that it is clear, unambiguous, and consistent across the world.

### Date + Time format

- **YYYY-MM-DDTHH:mm:ssZ**

- Example: `2025-09-07T12:45:30Z`
  
  - `T` = separator between date and time
  
  - `Z` = UTC (Zulu time)
  
  - Timezone offset can also be added, e.g. `2025-09-07T12:45:30+05:00` (Pakistan Standard Time)

## Unix Epoch

Jab unix OS develop huwa tha to software engineer ney 1, January 1970 00:00:00 UTC yani raat k 12 baje ko refrence point mana or isay agey time milliseconds mey calculate hona shuru huwa.

**1 January 1970, 00:00:00 UTC** se lekar ab tak jitne seconds guzre hain, uskay count ko hi Unix Epoch Kaha Jata hey.

Ye ek **starting point (zero time)** maana gaya hai operating systems aur programming me.

On this website you can view the number seconds has been passed from 1, January 1970 untill now: https://www.unixtimestamp.com/

# Date

In JavaScript, the `Date` object is used to work with dates and times. It represents a specific moment in time, measured in milliseconds since the Unix Epoch (January 1, 1970, 00:00:00 UTC).

Ager yeah line run kartey ho to apko time milay gi aik time string 

```js
 // Sun Sep 07 2025 14:32:36 GMT+0500 (Pakistan Standard Time)
 console.log(Date());
```

Ager app is traha likhtey ho to apko aik object wapis milay ga same text mey:

```js
//Sun Sep 07 2025 14:32:36 GMT+0500 (Pakistan Standard Time)
console.log(new Date())
```

You can confirm in the display the same time string and the related properties and methodsbrowser console by:

```js
console.dir(new Date())
```

It will show you the same time string and the related properties and mehtod of the Date Object.

### Date Creation

### Using milliseconds

```js
let epochDate = new Date(1678886400000); // Example timestamp
console.log(epochDate);
```

**NOTE:** The month always starts from 0 → January, 09 means (10 → October)

#### Creating a date from a date string using the Date Constructor

App sirf in do formate mey date pass kar saktey: `MM:DD:YYYY` or dosra `YYYY:MM:DD`

```js
let date = new Date('02/10/2003') // MM:DD:YYYY 
// OR 
let date2 = new Date('2003-10-02') // YYYY:MM:DD
```

**NOTE:** Slash ki jagah dash bhi use kar saktey app.

There is another intuitive way to create a using Date object is:

```js
let date = new Date("2 Oct 2025");
console.log(date);
```

or you can do this:

```js
let date = new Date("2 Octber 2025");
console.log(date);
```

You can also pass time with date:

```js
let date = new Date("2 October 2025 12:06:22")
```

### How to reverse a date string?

Ager apko kis date string ko reverse karna ho to yeah method use kar saktey

```js
let dateString = '02-10-2003'
console.log(dateString.split('-').reverse().join('-'))
```

The second method to reverse a date string is using destructing after splitting the string

```js
let dateString = "02/09/2003";
let [day, month, year] = dateString.split("/");
```

### Creating date and time from ISO string

- Agar tum date string me `Z` likho → iska matlab hota hai **UTC time**.
  
  ```js
  new Date("2003-10-02T13:00:00Z") // UTC 1:00 PM
  ```

- Agar tum offset likho `+05:00` → iska matlab hota hai wo specific timezone.
  
  ```js
  new Date("2003-10-02T13:00:00+05:00") // 1:00 PM in Pakistan
  ```

- Agar tum sirf `"2003-10-02T13:00:00"` likho bina `Z` ya offset ke → **JavaScript isko tumhare SYSTEM ke local time zone me samjhega**.

```js
new Date("2003-10-02T13:00:00") // System ka local timezone
```

- You can also mention milliseconds in iso string by appending a dot at the end of the seconds

```js
new Date("2003-10-02T13:00:00.600") // 600 milliseconds
```

**NOTE:** You cannot use slash `/` instead of `-` and `.` instead of `:` in an ISO date and time string; otherwise, JavaScript will consider this an invalid format.

### Using year, month, day, hours, minutes, seconds, milliseconds

```js
let date = new Date(2003, 10, 2, 2, 45, 12, 600);
console.log(date);
```

Yeh kaise parse hoga:

- `2003` → Year

- `10` → Month (November, kyunki 0 = Jan)

- `2` → Day (2nd November)

- `2` → Hours

- `45` → Minutes

- `12` → Seconds

- `600` → Milliseconds

Result → **2 November 2003, 02:45:12.600 (local timezone ke hisaab se)**

## getTime()

Both methods shall return time in milliseconds from the Unix epoch (1 January 1970 00:00:00 UTC)

```javascript
let date = new Date()
console.log(Date.now(), date.getTime())
```

### toString()

Local timezone k ander date string return karta hey.

```js
let date = new Date()
console.log(date.toString())
```

### toLocalString()

Yeh date ko **aapke local computer ke timezone** aur **language/locale** ke hisaab se ek **string** bana deta hai.

```js
let date = new Date()
date.toLocaleTimeString(locales, options)
```

#### Parameters

**locales**: Pehla argument aik BCP 47 language tag ek **code** hai jo batata hai ke **kaunsi bhasha aur kis country/region ke rules** ke mutabiq text ya date/time format karna hai. For example, `ur-PK` represents Urdu Pakistan.

**options:**

Mazeed bhi options heyn per yaha kuxh example diye hoee heyn

```js
date.toLocaleString("en-US", {
    weekday: "long",
    month: "long",
    day: "numeric",
  })
```

### toLocalDateString()

Yeah, sirf date ko local timezone or language sensitive format mey dhikata hey

**Syntax:**

```js
toLocaleDateString()
toLocaleDateString(locales)
toLocaleDateString(locales, options)
```

```js
const date = new Date("2 October 2003");

document.querySelector("#date").innerHTML = dat
e.toLocaleDateString("ur-PK", {
  dateStyle: "full",
});
```

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-09-25-15-56-49-image.png)

Baki argument bhi heyn jesay `weekday` , `month` etc.

### toLocalTimeString()

Yeah, sirf time ko language or country's k hisab say localtimzone mey display karta hey

**Syntax:**

```js
toLocaleTimeString()
toLocaleTimeString(locales)
toLocaleTimeString(locales, options)
```

**Example**

```js
const date = new Date();

document.querySelector("#date").innerHTML 
= date.toLocaleTimeString("ur-PK", {
  timeStyle: "full",
});
```

![](C:\Users\mrasi\AppData\Roaming\marktext\images\2025-09-25-16-08-53-image.png)

Samajh gaya 👍 tum chahte ho ke **JavaScript Date object ke tamam getter aur setter methods** ek jagah list hoon, unke examples ke sath, aur agar koi exception / khas note ho to woh bhi mention ho.

---

# JavaScript Date Getters & Setters

## 🔹 **Getter Methods (values read karne ke liye)**

Ye methods date/time se alag-alag parts nikalte hain.

1. **`getFullYear()`**
   
   - Pura year return karta hai (4 digits).
   
   - Example:
     
     ```js
     let d = new Date("2003-10-02");
     console.log(d.getFullYear()); // 2003
     ```
   
   - **Note:** Always Gregorian year deta hai.

2. **`getMonth()`**
   
   - Month (0–11) return karta hai.
   
   - Example:
     
     ```js
     console.log(d.getMonth()); // 9 (October)
     ```
   
   - ⚠️ **Exception/Note:** 0 = January, 11 = December.

3. **`getDate()`**
   
   - Month ka din return karta hai (1–31).
   
   - ```js
     console.log(d.getDate()); // 2
     ```

4. **`getDay()`**
   
   - Week ka din return karta hai (0–6).
   
   - Example:
     
     ```js
     console.log(d.getDay()); // 4 (Thursday)
     ```
   
   - **Note:** 0 = Sunday.

5. **`getHours()`**
   
   - Hour return karta hai (0–23).

6. **`getMinutes()`**
   
   - Minutes return karta hai (0–59).

7. **`getSeconds()`**
   
   - Seconds return karta hai (0–59).

8. **`getMilliseconds()`**
   
   - Milliseconds (0–999).

9. **`getTime()`**
   
   - Timestamp return karta hai (ms since 1 Jan 1970 UTC).
   
   - ```js
     console.log(d.getTime()); // 1065052800000
     ```

10. **`getTimezoneOffset()`**
    
    - Local time aur UTC ka difference minutes mein.
    
    - ```js
      console.log(d.getTimezoneOffset()); // e.g., -300
      ```
    
    - **Note:** Negative matlab local time UTC se aage hai.

11. **UTC versions:**
    
    - `getUTCFullYear()`, `getUTCMonth()`, `getUTCDate()`, `getUTCDay()`,  
      `getUTCHours()`, `getUTCMinutes()`, `getUTCSeconds()`, `getUTCMilliseconds()`
    
    - Ye same getters hain lekin **UTC zone ke hisaab se** value dete hain.

---

## 🔹 **Setter Methods (values change karne ke liye)**

Ye methods existing Date object ko modify karte hain.

1. **`setFullYear(year, month?, date?)`**
   
   - Year set karta hai (aur optional month/date).
   
   - Example:
     
     ```js
     d.setFullYear(2025);
     console.log(d); // 2025-10-02T...
     ```
   
   - **Exception:** Agar month/date invalid ho jaye to auto-adjust kar lega.
     
     ```js
     d.setFullYear(2025, 13, 32); // month 13 → next year adjust hoga
     ```

2. **`setMonth(month, date?)`**
   
   - Month (0–11).
   
   - Invalid date ho to auto-adjust.

3. **`setDate(date)`**
   
   - Day of month (1–31).
   
   - Out of range → next month adjust.
   
   - ```js
     d.setDate(35); // move to next month
     ```

4. **`setHours(hours, min?, sec?, ms?)`**
   
   - 0–23 range.
   
   - Invalid → adjust automatically.

5. **`setMinutes(min, sec?, ms?)`**
   
   - 0–59 range.

6. **`setSeconds(sec, ms?)`**
   
   - 0–59 range.

7. **`setMilliseconds(ms)`**
   
   - 0–999.

8. **`setTime(ms)`**
   
   - Direct timestamp set karna (ms since 1970 UTC).

9. **UTC versions:**
   
   - `setUTCFullYear()`, `setUTCMonth()`, `setUTCDate()`,  
     `setUTCHours()`, `setUTCMinutes()`, `setUTCSeconds()`, `setUTCMilliseconds()`
   
   - Ye same setters hain, bas **UTC ke hisaab se set karte hain.**

---

## ⚠️ Important Notes & Exceptions

- Agar **invalid date** pass kar do (like `new Date("invalid")`) to getters `NaN` return karte hain.

- Setters out-of-range values ko **roll over** kar dete hain instead of error.
  
  - Example:
    
    ```js
    let d = new Date("2003-01-31");
    d.setMonth(1); // February 31 → auto-adjust → March 3
    console.log(d.toDateString()); // Mon Mar 03 2003
    ```

- `getYear()` **deprecated** hai → use `getFullYear()`.
