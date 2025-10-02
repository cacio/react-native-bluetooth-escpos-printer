# @cacio/react-native-bluetooth-escpos-printer

> Fork ajustado de [januslo/react-native-bluetooth-escpos-printer](https://github.com/januslo/react-native-bluetooth-escpos-printer)
> Compatível com Gradle atualizado e Android 13+.

[![npm version](https://badge.fury.io/js/%40cacio%2Freact-native-bluetooth-escpos-printer.svg)](https://www.npmjs.com/package/@cacio/react-native-bluetooth-escpos-printer)

Biblioteca **React Native** para integração com impressoras Bluetooth ESC/POS & TSC.
Ideal para recibos, etiquetas e integração com dispositivos Android.

---

## ✨ Features
- Suporte a **ESC/POS** (recibos) e **TSC** (etiquetas)
- Gerenciamento de Bluetooth (parear, conectar, listar dispositivos)
- Compatível com **TypeScript**
- Testado principalmente em **Android**
- Em desenvolvimento ativo

---

## 📦 Instalação

### 1. Instalar pacote
```bash
npm install @cacio/react-native-bluetooth-escpos-printer
# ou
yarn add @cacio/react-native-bluetooth-escpos-printer
```

### 2. Link (apenas RN < 0.60)
```bash
react-native link @cacio/react-native-bluetooth-escpos-printer
```

Para **React Native 0.60+**, o autolinking cuida disso automaticamente ✅.

### 3. Importar no projeto
```ts
import {
  BluetoothManager,
  BluetoothEscposPrinter,
  BluetoothTscPrinter
} from '@cacio/react-native-bluetooth-escpos-printer';
```

---

## 🚀 Uso rápido

### Verificar se Bluetooth está ativo
```ts
const enabled = await BluetoothManager.checkBluetoothEnabled();
console.log(enabled); // true | false
```

### Ativar e listar dispositivos pareados
```ts
const devices = await BluetoothManager.enableBluetooth();
```

### Escanear novos dispositivos
```ts
const { found, paired } = JSON.parse(await BluetoothManager.scanDevices());
```

### Conectar a um dispositivo
```ts
await BluetoothManager.connect("XX:XX:XX:XX:XX:XX");
```

### Imprimir texto simples
```ts
await BluetoothEscposPrinter.printText("Olá, mundo!\n\r", {
  encoding: 'GBK',
  widthtimes: 1,
  heigthtimes: 1,
  fonttype: 0,
});
```

### Imprimir etiqueta TSC
```ts
await BluetoothTscPrinter.printLabel({
  width: 40,
  height: 30,
  text: [
    {
      text: "Etiqueta Teste",
      x: 20,
      y: 20,
      fonttype: BluetoothTscPrinter.FONTTYPE.SIMPLIFIED_CHINESE,
      rotation: BluetoothTscPrinter.ROTATION.ROTATION_0,
      xscal: BluetoothTscPrinter.FONTMUL.MUL_1,
      yscal: BluetoothTscPrinter.FONTMUL.MUL_1,
    }
  ],
});
```

---

## 📚 APIs disponíveis

- [BluetoothManager](#bluetoothmanager) → gerenciamento de Bluetooth
- [BluetoothTscPrinter](#bluetoothtscprinter) → impressão de etiquetas
- [BluetoothEscposPrinter](#bluetoothescposprinter) → impressão de recibos ESC/POS

---

## 🔧 BluetoothManager
Funções principais:
- `checkBluetoothEnabled()` → verifica se Bluetooth está ativo
- `enableBluetooth()` → ativa e retorna dispositivos pareados
- `scanDevices()` → procura novos dispositivos
- `connect(address)` → conecta a um dispositivo
- `disconnect(address)` → desconecta
- `getConnectedDeviceAddress()` → retorna o endereço atual
- `unpair(address)` → desfaz pareamento

Eventos emitidos:
`EVENT_DEVICE_ALREADY_PAIRED`, `EVENT_DEVICE_FOUND`, `EVENT_CONNECTED`, `EVENT_CONNECTION_LOST`, etc.

---

## 🖨️ BluetoothTscPrinter
Usado para **etiquetas**.
Principais métodos:
- `printLabel(options)` → imprime etiqueta (texto, QRCode, imagem, etc.)

---

## 🧾 BluetoothEscposPrinter
Usado para **recibos ESC/POS**.
Principais métodos:
- `printerInit()`
- `printText(text, options)`
- `printColumn(cols, aligns, texts, options)`
- `printQRCode(content, size, correctionLevel)`
- `printBarCode(...)`
- `printPic(base64, options)`
- `cutOnePoint()`
- `openDrawer(pin, onTime, offTime)`

---

## 🐞 Contribuição
Achou um bug ou precisa de uma melhoria?
Abra uma [issue](https://github.com/seu-usuario/react-native-bluetooth-escpos-printer/issues) ou envie um PR 🚀

---

## 📜 Licença
MIT © [cacio](https://github.com/seu-usuario)
