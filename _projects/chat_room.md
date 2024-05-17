---
layout: post
title: Chat aplikace (Sockets.io + room)
category: "html"
order: 7
---

# Rozdělení do skupin (room)

Cílem tohoto úkolu bude se seznámit s možností rozdělit klienty Socket.io do skupin. V Socket.io se této funkcionalitě říká [rooms](https://socket.io/docs/v3/rooms/).

> **Úkol 1 - Přidat text box pro zadání room**
> Do `init div` přidejte text box pro zadání jména `room` (tzn. jméno skupiny ve které bude). Po stisku OK tlačítka se jméno `room` pošle na server a na serveru přidejte klienta do skupiny `room` s pomocí příkazu `socket.join(room);`.

> **Úkol 2 - Rozesílání zpráv pouze uživatelům v dané room**
> Klient nyní přidá hodnotu `room` do JSON zprávy po stisku SEND. Server pošle zprávu pouze na klienty v dané skupině s pomocí příkazu `socket.to(room).emit("chat_message", msg)`.
