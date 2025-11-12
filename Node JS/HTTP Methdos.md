## GET

 Get a representation of this resource.

## DELETE

 Destroy this resource.

## POST

Create a new resource underneath this one, based on the given representation.

## PUT

 Replace this state of this resource with the one described in the given representation.
 These two methods are mostly used as a client explores an API:

## HEAD

 Get the headers that would be sent along with a representation of this resource, but
 not the representation itself.

## OPTIONS

 Discover which HTTP methods this resource responds to.

## PATCH

Representations can get really big. “Modify the representation and PUT it back” is a simple rule, but if you just want to change one little bit of resource state, it can be pretty wasteful.

It would be nice if you could just send the server the parts of the document you want to change. The PATCH method allows for this. Instead of PUTting a full representation, you can create a special “diff” representation and send it to the server as the payload of PATCH request.

## Idempotance

**Idempotence** (Aksariyat-pasandi/Na-badalna) HTTP methods mein ek aisi khaasiyat (property) hai jiska matlab hai ke agar aap uss request ko **ek baar bhejain ya ek se zyada baar bhejain**, toh **server par resource ki halat (state) par asar (effect) hamesha ek jaisa** hi rahega.

Matlab, request ko dohraane (repeating) se naye ya mukhtalif (different) natije nahi milte.
