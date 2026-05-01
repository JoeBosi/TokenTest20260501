# Project agents

## SolidityAgent
- Ruolo: Progetta e implementa smart contract in Solidity usando OpenZeppelin.
- Obiettivi:
  - Creare un token ERC20 **aggiornabile** usando i contratti upgradeable di OpenZeppelin.
  - Usare pattern proxy (UUPS o Transparent) con inizializzatore al posto del costruttore.
  - Implementare funzioni di `mint` e `burn` con regole di sicurezza chiare.
- Regole di sicurezza:
  - `mint` consentito solo a ruoli autorizzati (`MINTER_ROLE`) o `onlyOwner`, mai pubblico.
  - `burn` consentito solo sul proprio saldo (`msg.sender`) o con controlli espliciti.
  - Usare `AccessControl` o `Ownable` per la gestione dei permessi.
  - Prevedere eventi per `Mint`, `Burn`, `RoleGranted`, `RoleRevoked`.
- Cartella di lavoro: `./solidity`

## SolidityTestAgent
- Ruolo: Scrive e mantiene i test per gli smart contract.
- Obiettivi:
  - Testare correttamente `mint`, `burn`, trasferimenti e permessi.
  - Verificare che solo gli account autorizzati possano chiamare `mint`.
  - Verificare che `burn` non permetta di bruciare più del saldo disponibile.
  - Testare l’aggiornabilità del contratto (deploy proxy, upgrade, stato preservato).
- Cartella di lavoro: `./solidity/test`

## FrontendAgent
- Ruolo: Implementa il frontend per la gestione del token.
- Obiettivi:
  - Creare una UI per:
    - mint (solo per account autorizzati),
    - burn (sul proprio saldo),
    - lettura balance, totalSupply e altri attributi,
    - chiamata dei metodi di amministrazione se previsti.
  - Usare React (o Vite+React) ed `ethers.js` (o libreria equivalente).
  - Collegarsi al contratto tramite ABI e address del proxy.
- Cartella di lavoro: `./frontend`

## IntegrationAgent
- Ruolo: Coordina integrazione tra smart contract e frontend.
- Obiettivi:
  - Documentare il flusso: deploy del proxy → address → configurazione nel frontend.
  - Mantenere aggiornati ABI e indirizzi nel frontend dopo ogni upgrade.
  - Aggiornare il README con i comandi per:
    - deploy,
    - test,
    - avvio del frontend.
