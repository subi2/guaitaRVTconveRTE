<!--
  Guaita Apps - Suite d'eines autònomes per a arquitectura, BIM i documentació.
  Copyright (c) 2026 Jordi Subirós
  GNU Affero General Public License v3.0
  See LICENSE file for details
-->

# GUAITA·RVT — Guaita RVT conveRTE

`Manual d'ús`

## Canvia un projecte RVT a *plantilla* RTE (i a l'inrevés).

Guaita RVT conveRTE inverteix el tipus intern d'un fitxer —de projecte `.rvt` a plantilla `.rte` o al revés— modificant un únic marcador dins del document, tot dins del teu navegador i sense enviar el fitxer enlloc.

## Contingut

1. [Què és](#01--introducció)
2. [RVT i RTE](#02--projecte-i-plantilla)
3. [Com començar](#03--com-començar)
4. [La interfície](#04--la-interfície)
5. [La detecció](#05--com-detecta-el-tipus)
6. [Convertir i desar](#06--convertir-i-desar)
7. [Límits i garanties](#07--límits-i-garanties)
8. [Problemes](#08--resolució-de-problemes)

---

## 01 · Introducció

### Un convertidor de tipus de fitxer RVT/RTE en una sola pàgina

Un mateix model es pot desar com a **projecte** (extensió `.rvt`) o com a **plantilla** (extensió `.rte`). No n'hi ha prou de canviar l'extensió al nom del fitxer: dins del document hi ha un marcador intern que en determina el tipus, i és el que l'aplicació llegeix en obrir-lo.

Guaita RVT conveRTE localitza aquest marcador i el capgira. És un únic fitxer HTML que s'obre a qualsevol navegador modern; no cal instal·lar res.

Tot el processament passa dins del teu navegador. El fitxer no s'envia a cap servidor, així que pots treballar amb models confidencials i sense connexió.

| | |
|---|---|
| 📤 **Sense servidor** | El fitxer no surt del teu equip; es processa en local. |
| ✏️ **Canvi mínim** | Només toca el marcador de tipus, quatre bytes. |
| ✅ **Verificat** | Rellegeix el fitxer després del canvi per confirmar-lo. |
| 🔁 **Bidireccional** | Projecte a plantilla i plantilla a projecte. |

## 02 · Projecte i plantilla

### Què separa un .rvt d'un .rte

Tots dos són el mateix format de fitxer intern (un contenidor OLE2/CFBF). La diferència de tipus viu al **Last Save Path** desat dins l'apartat `BasicFileInfo` del document: hi apareix l'extensió del fitxer (`.rvt` o `.rte`) i és aquest text el que marca la naturalesa del document.

| Tipus | Extensió | Ús |
|---|---|---|
| **Projecte** | `.rvt` | El model de treball habitual, amb el seu contingut i historial. |
| **Plantilla** | `.rte` | Punt de partida per a nous projectes: estils, famílies i configuracions predefinides. |

> [!NOTE]
> **Per què no n'hi ha prou de reanomenar**
>
> Si només canvies l'extensió del nom del fitxer a l'explorador, l'aplicació continua veient el tipus intern original i pot rebutjar-lo o obrir-lo com el tipus que no toca. Aquesta eina canvia el marcador de dins.

## 03 · Com començar

### Dues maneres de carregar el fitxer

1. **Arrossega i deixa anar** el fitxer `.rvt` o `.rte` sobre la zona de càrrega central.
2. O **fes clic a la zona de càrrega** («Arrossega el fitxer aquí, o clica per seleccionar-lo») per obrir el selector de fitxers del sistema.

Un cop carregat, l'eina el llegeix a l'instant i mostra la fitxa amb el tipus detectat i la proposta de conversió.

> [!NOTE]
> **Extensions acceptades**
>
> El selector filtra per `.rvt` i `.rte`. Assegura't que el fitxer és realment un document RVT o RTE; si no ho és, l'eina t'avisarà.

## 04 · La interfície

### On és cada cosa

La finestra és una única targeta vertical. El mapa següent en mostra la disposició de dalt a baix:

| Zona | Contingut |
|---|---|
| **Capçalera** | «Guaita RVT conveRTE» amb la descripció |
| **Zona de càrrega** | Àrea per arrossegar o clicar. Mostra les extensions `.rvt` i `.rte` i recorda que tot es processa en local. |
| **Origen** | El fitxer carregat amb la seva etiqueta (PROJECTE · RVT o PLANTILLA · RTE). |
| **Fletxa i destí** | La conversió proposada, amb un camp per editar el nom de sortida i l'extensió resultant fixada. |
| **Avís** | Nota groga: eina experimental, cal verificar sempre el resultat. |
| **Peu** | Botó de conversió · missatge d'estat un cop descarregat el fitxer |

## 05 · Com detecta el tipus

### Llegir abans de tocar res

En carregar el fitxer, l'eina obre l'estructura interna del document i busca l'extensió (`.rvt` o `.rte`) dins del Last Save Path de `BasicFileInfo`. Segons el que hi troba, en dedueix el tipus:

- Si hi apareix `.rvt`, el fitxer és un **projecte**.
- Si hi apareix `.rte`, el fitxer és una **plantilla**.

A la fitxa hi veuràs la **mida** del fitxer i, en mode tècnic, els **offsets** exactes on s'ha trobat el marcador. La targeta et proposa automàticament la conversió cap al tipus contrari.

> [!WARNING]
> **Quan no es pot determinar**
>
> Si dins del fitxer no hi ha cap extensió reconeixible, o n'hi ha de contradictòries, l'eina no pot decidir el tipus i t'ho diu amb un missatge d'error, sense modificar res.

## 06 · Convertir i desar

### Un clic, un fitxer nou descarregat

1. **Revisa el nom de sortida.** Al camp editable de la banda de destí pots canviar el nom base; l'extensió resultant (`.rvt` o `.rte`) queda fixada segons la conversió.
2. **Prem el botó de conversió.** El text del botó indica exactament l'acció, per exemple «Converteix a plantilla (.rte) → nom.rte».
3. L'eina fa el canvi, **torna a llegir el fitxer per verificar** que el marcador s'ha actualitzat i **descarrega** el resultat automàticament al navegador.

Quan acaba, apareix un missatge verd de confirmació amb el nom del fitxer descarregat i la nota que el tipus s'ha verificat després del canvi.

> [!NOTE]
> **Què canvia exactament**
>
> Només se substitueix el text de l'extensió dins `BasicFileInfo` (quatre bytes), amb la mateixa llargada. No es toca l'historial de desats, ni cap comptador, ni la resta del contingut del model, que queda idèntic bit a bit.

## 07 · Límits i garanties

### Fes-ho amb cap

El fitxer d'origen no es modifica: sempre obtens un **fitxer nou descarregat**, així que conserves l'original per si de cas. Tot i això, treballes amb dades reals: mantén una còpia de seguretat i comprova sempre el resultat.

> [!CAUTION]
> **Eina experimental**
>
> L'aplicació s'ha concebut amb finalitats educatives. Encara que el canvi és mínim i verificat, **és imprescindible obrir el fitxer resultant amb l'aplicació d'autoria** per confirmar que es comporta com esperes abans de fer-lo servir en producció.

## 08 · Resolució de problemes

### Si alguna cosa no va

<details>
<summary>«No és un fitxer OLE2/CFBF vàlid»</summary>

El fitxer carregat no té l'estructura interna d'un document RVT/RTE. Comprova que és realment un `.rvt` o `.rte` i que no està malmès o comprimit.
</details>

<details>
<summary>«No s'ha pogut determinar el tipus»</summary>

Dins del Last Save Path de `BasicFileInfo` no hi ha cap extensió reconeixible, o n'hi ha de contradictòries. L'eina no pot decidir el tipus i no toca res. Prova de desar el fitxer de nou des de l'aplicació d'origen i torna-ho a intentar.
</details>

<details>
<summary>El navegador no descarrega el fitxer</summary>

Alguns navegadors bloquegen les descàrregues automàtiques. Revisa la barra de descàrregues i els permisos del lloc. Si has obert l'HTML des d'un entorn molt restringit, prova un navegador d'escriptori estàndard.
</details>

<details>
<summary>L'aplicació no obre el fitxer convertit</summary>

Recorda que és una eina experimental. Torna a comprovar que la conversió tenia sentit (un projecte real cap a plantilla, o al revés) i, si cal, parteix de l'original i torna-ho a provar. Verifica sempre el resultat.
</details>

---

**GUAITA RVT conveRTE**
Convertidor de tipus de fitxer RVT/RTE · SBS BIM Consulting
