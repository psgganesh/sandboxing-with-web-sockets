# Sandboxing with api websockets 🔌 💬
AWS simple SAM CLI template & front-end project to demonstrate API Websockets and SAM CLI.

> This project uses yarn as a package manager for quicker response times on CLI, you may feel free to replace the word `yarn` with `npm` if you want to !

## Prerequsites
Ensure you have node and npm installed on your system to run this project
- node - v16.xx.x
- npm - 8.x.x

## Installing yarn globally
```sh
npm i -g yarn # Ignore if yarn is already installed
```
## Project setup
```sh
# Installs all front-end dependencies
yarn        # OR npm install

# Runs the sam CLI to prepare AWS resources
yarn setup  # OR npm run setup
```
### Run the front-end project on localhost
```sh
yarn start # OR npm run start
```

## Testing

On the console, connect to your published API endpoint by executing the following command:
```sh
wscat -c wss://{YOUR-API-ID}.execute-api.{YOUR-REGION}.amazonaws.com/{STAGE}
```

To test the sendMessage function, send a JSON message like the following example. The Lambda function sends it back using the callback URL

```sh
wscat -c wss://{YOUR-API-ID}.execute-api.{YOUR-REGION}.amazonaws.com/prod
connected (press CTRL+C to quit)
> {"action":"sendmessage", "data":"hello world"}
```
---
## License Summary
This sample code is made available under a modified MIT license. See the LICENSE file.