# PageCrypt - Password Protected HTML Pages

> A CLI to add client-side password-protection for HTML files

Inspired by [MaxLaumeister/PageCrypt](https://github.com/MaxLaumeister/PageCrypt). Thanks for sharing an excellent starting point to create this CLI!

## Usage

### CLI

Encrypt a single HTML-file with one command:

```sh
npx pagecrypt [input.html] [output.html] [password]
```

### Automate `pagecrypt` in your build process

```sh
npm i -D pagecrypt
```

package.json:

```json
{
    "devDependencies": {
        "pagecrypt": "^1.2.0"
    },
    "scripts": {
        "build": "...",
        "postbuild": "pagecrypt index.html encrypted.html password"
    }
}
```

### Node.js API

You can use `pagecrypt` in your Node.js scripts:

#### `encrypt(inputFile: string, outputFile: string, password: string): Promise<void>`

```js
import { encrypt } from 'pagecrypt'

// Encrypt a HTML file and write to the filesystem
await encrypt('input.html', 'output.html', 'password')
```

#### `encryptHTML(inputHTML: string, password: string): Promise<string>`

```js
import { encryptHTML } from 'pagecrypt'

// Encrypt a HTML string and return an encrypted HTML string.
// Write it to a file or send as an HTTPS response.
const encryptedHTML = await encryptHTML(
    `<!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8">
        </head>
        <body>
            Secret
        </body>
    </html>
`,
    'password',
)
```

---

## Development

The project consists of four parts:

-   `/web` - Web frontend for public webpage (`decrypt-template.html`). Built using Vite & Tailwind CSS.
-   `/index.js` - pagecrypt main library.
-   `/cli.js` - pagecrypt CLI.
-   `/test` - testing setup

## Setup a local development environment

1.  Install Node.js >= 15.0.0
2.  Run `npm install` in project root.
3.  Install and use [`mkcert`](https://github.com/FiloSottile/mkcert) to generate local certificates to enable HTTPS for the development server. For example `mkcert localhost 192.168.1.32` to generate a two files ending with `*.pem`.
4.  Update `vite.config.js` to load the generated `*.pem` files in the `https` section.
5.  To use `npm run serve`, also update to the correct `*.pem` filenames in the npm script.

## Testing

`npm test` will run basic tests for JS API and CLI. Verify results by opening `test/out-js.html` and `test/out-cli.html` in your browser.

---

**Welcome to submit your pull requests!**
