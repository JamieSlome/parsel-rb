# parsel

[![Code Climate](https://codeclimate.com/github/fnando/parsel-rb.png)](https://codeclimate.com/github/fnando/parsel-rb)
[![Build Status](https://travis-ci.org/fnando/parsel-rb.svg)](https://travis-ci.org/fnando/parsel-rb)
[![Gem](https://img.shields.io/gem/v/parsel.svg)](https://rubygems.org/gems/parsel)
[![Gem](https://img.shields.io/gem/dt/parsel.svg)](https://rubygems.org/gems/parsel)

Encrypt and decrypt data with a given key.

This library was created to allow an easy data
exchange between Ruby and Node.js.

Check it out the Node.js counter-part: <http://github.com/fnando/parsel-js>.

## Installation
asd
    gem install parsel

## Usage

```ruby
require "parsel"

secret_key = "mysupersecretkeythatnobodyknowsabout"
encrypted = Parsel.encrypt(secret_key, "hello from ruby!")
decrypted = Parsel.decrypt(secret_key, encrypted)
```

You can also use Marshal for encrypting/decrypting objects. Notice that this isn't supported by Node.js.

```ruby
require "parsel"

data = {user_id: 1234}

secret_key = "mysupersecretkeythatnobodyknowsabout"
encrypted = Parsel::Marshal.encrypt(secret_key, data)

decrypted = Parsel::Marshal.decrypt(secret_key, encrypted)
#=> {user_id: 1234}
```

Alternatively you can use `JSON` as your serializer.

```ruby
require "parsel"

data = {user_id: 1234}

secret_key = "mysupersecretkeythatnobodyknowsabout"
encrypted = Parsel::JSON.encrypt(secret_key, data)

decrypted = Parsel::JSON.decrypt(secret_key, encrypted)
#=> {"user_id" => 1234}
```

### Custom Cipher IV

![Make sure you use a 16-chars long if you're going to exchange data with parsel-js.](http://messages.hellobits.com/warning.svg?message=Make%20sure%20you%20use%20a%2016-chars%20long%20if%20you're%20going%20to%20exchange%20data%20with%20parsel-js.)

By default, this library uses a built-in IV. You may want to change that.

You can globally change the IV like the following:

```ruby
Parsel.default_iv = SecureRandom.hex(100)
```

You can also pass the IV to encrypt/decrypt methods.

```ruby
Parsel.encrypt(secret_key, iv, data)
Parsel.decrypt(secret_key, iv, data)
```

**NOTE:** If you're going to use <http://github.com/fnando/parsel-js> to exchange data, you have to use a 16-chars long IV. Node.js will fail with different lengths.

## Maintainer

- Nando Vieira (<http://nandovieira.com.br>)

## License

(The MIT License)

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
