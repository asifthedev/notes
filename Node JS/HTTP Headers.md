## What is Hypermedia?

Hypermedia is the general term for things like `HTML links` and `forms`: the techniques a server uses to explain to a client what it can do next.

### What is HATEOAS?

**HATEOAS** ka matlab hai: **Hypermedia as the Engine of Application State**.

Yeh REST (Representational State Transfer) architecture style ka **sabse ahem (most important)** aur aksar **misunderstood** (galat samjha jane wala) usool (constraint) hai\

Server har response (jawab) mein **data** ke saath-saath, **woh links** bhi bhejta hai jo yeh batate hain ke is data ke saath ab **client kaunsa agla action** le sakta hai.

#### Why it's important?

In REST terms, putting information about URL construction in separate humanreadable documents violates the principles of connectedness and self-descriptive messages.

In REST terms, putting information about URL construction in separate human
readable documents violates the principles of connectedness and self descriptive messages.

## What is Resource?

Anything that you can assigne a URL and store on the computer is the only constraint on rerouce. Otherwise resource can be anyting important enough to referenced as thing.

## What is Representaion

Thats a representation—a machine-readable explanation of the current state of a resource.

A representation can be any machine-readable document containing any information about a resource.

Resource ki Woh Shakal ya Format jo Client ko Bheji Jati Hai.

Jab client (jaisay aapka browser ya mobile app) server se kisi **Resource** ko **GET** karta hai, toh server **asli data** ko jaisa woh data base mein hai, waisa ka waisa nahi bhejta.

Balkay, server us asli data ki **ek copy** ya **ek jhalak** (snapshot) banata hai aur usay ek khas **format (shakal)** mein **client ke liye represent** karta hai. Yahi **Representation** hai.

## States

### Application State

Jis page k uper app abhi heyn woh hey application state client wali tarf

In REST term which page are you on is known as aplication state. 


