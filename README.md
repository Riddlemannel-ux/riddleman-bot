# riddleman-bot
const { default: makeWASocket, useSingleFileAuthState } = require("@whiskeysockets/baileys")

async function startBot() {
    const sock = makeWASocket({
        printQRInTerminal: true
    })

    sock.ev.on("messages.upsert", async (m) => {
        const msg = m.messages[0]
        if (!msg.message) return

        const text = msg.message.conversation || msg.message.extendedTextMessage?.text

        if (text === "hi") {
            await sock.sendMessage(msg.key.remoteJid, { text: "Hello 👋 I am your bot" })
        }
    })
}

startBot()