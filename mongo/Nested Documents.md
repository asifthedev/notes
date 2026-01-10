## Nested Documents

Ager kis document k ander koee field ki value bhi document ho to ham isay nested documetn kaheyn gey yani documents inside a document, for example:

```mongodb
{
    name: "Asif",
    address: {city: "Vehari", country: "Pakistan"}
}
```

## Notes

MongoDB **maximum 16 MB per document** allow karta hai. Yeh ek **fixed** limit hai — isse zyada ka single document save nahi hota.

**Nesting limit** kelye koee official fixed number nhi hey, but practical safe limit ≈ **100 levels**

## Filtering Nested Documents

Show me the documents where city is Vehari

```mongodb
db.users.find({"address.city": "Vehari"})
```


