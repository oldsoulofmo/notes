---
title: "Separating the user interface from program logic - Java Programming"
source: "https://java-programming.mooc.fi/part-6/2-separating-user-interface-from-program-logic"
author:
  - "[[University of Helsinki]]"
published:
created: 2025-02-19
description: "Helsingin yliopiston kaikille avoin ja ilmainen ohjelmoinnin perusteet opettava verkkokurssi. Kurssilla perehdytään nykyaikaisen ohjelmoinnin perusideoihin sekä ohjelmoinnissa käytettävien työvälineiden lisäksi algoritmien laatimiseen. Kurssille osallistuminen ei vaadi ennakkotietoja ohjelmoinnista."
tags:
  - "clippings"
---
The main point here is that changes made inside the class WordSet don't affect the class UserInterface. This is because the user interface uses WordSet through the methods that it provides — these are called its public interfaces.