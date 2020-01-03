[@poppinss/cookie](../README.md) › ["Cookie"](_cookie_.md)

# External module: "Cookie"

## Index

### Type aliases

* [CookieOptions](_cookie_.md#cookieoptions)

### Functions

* [pack](_cookie_.md#pack)
* [parse](_cookie_.md#parse)
* [serialize](_cookie_.md#serialize)
* [unpack](_cookie_.md#unpack)

## Type aliases

###  CookieOptions

Ƭ **CookieOptions**: *object*

*Defined in [Cookie.ts:13](https://github.com/poppinss/cookie/blob/7f8d8f0/src/Cookie.ts#L13)*

#### Type declaration:

## Functions

###  pack

▸ **pack**(`value`: any, `secretKey?`: undefined | string): *null | string*

*Defined in [Cookie.ts:37](https://github.com/poppinss/cookie/blob/7f8d8f0/src/Cookie.ts#L37)*

Pack a value to be saved as a cookie string. If `secretKey` is
defined, then cookie will be signed to avoid client side
tampering.

When setting the cookie header, it is recommended to [serialize](_cookie_.md#serialize) method
instead.

**`example`** 
```ts
pack('hello world', 'a-long-secret-to-sign-cookie')
pack({ hello: 'world' }, 'a-long-secret-to-sign-cookie')
```

**Parameters:**

Name | Type |
------ | ------ |
`value` | any |
`secretKey?` | undefined &#124; string |

**Returns:** *null | string*

___

###  parse

▸ **parse**(`cookieHeader`: string, `secretKey?`: undefined | string): *object*

*Defined in [Cookie.ts:126](https://github.com/poppinss/cookie/blob/7f8d8f0/src/Cookie.ts#L126)*

Parse cookie header and return an object of cookies as `key/value` pair. The
output of this method has two top level objects explained below:

## Signed cookies
An object of cookies that are successfully verified and not being tampered.

## Plain cookies
An object of cookies that were not signed initially via [serialize](_cookie_.md#serialize) method.

**`example`** 
```ts
const result = parse(req.headers['cookie'], 'a-long-secret-to-sign-cookie')

result.signedCookies
result.plainCookies
```

**Parameters:**

Name | Type |
------ | ------ |
`cookieHeader` | string |
`secretKey?` | undefined &#124; string |

**Returns:** *object*

___

###  serialize

▸ **serialize**(`key`: string, `value`: any, `secretKey?`: undefined | string, `options?`: Partial‹[CookieOptions](_cookie_.md#cookieoptions)›): *string | null*

*Defined in [Cookie.ts:165](https://github.com/poppinss/cookie/blob/7f8d8f0/src/Cookie.ts#L165)*

Serializes a key/value pair to a string, which is supposed
to be set as `Set-Cookie` header value.

**`example`** 
```ts
const serialized = serialize('session-id', '1', 'a-long-secret-to-sign-cookie', {
  // optional config
})
res.setHeader('set-cookie', serialized)
```

**Parameters:**

Name | Type |
------ | ------ |
`key` | string |
`value` | any |
`secretKey?` | undefined &#124; string |
`options?` | Partial‹[CookieOptions](_cookie_.md#cookieoptions)› |

**Returns:** *string | null*

___

###  unpack

▸ **unpack**(`value`: string, `secretKey?`: undefined | string): *null | object*

*Defined in [Cookie.ts:69](https://github.com/poppinss/cookie/blob/7f8d8f0/src/Cookie.ts#L69)*

Unpack, previously packed cookie value. If cookie was signed and `secretKey` is
not passed to this method, then the signed value will be returned as a plain
cookie.

**`example`** 
```ts
const packed = pack('hello world', 'a-long-secret-to-sign-cookie')
unpack(packed, 'a-long-secret-to-sign-cookie') // hello-world
```

**Parameters:**

Name | Type |
------ | ------ |
`value` | string |
`secretKey?` | undefined &#124; string |

**Returns:** *null | object*