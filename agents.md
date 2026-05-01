# Project agents

## SolidityAgent
- Ruolo: Progetta e implementa smart contract in Solidity usando OpenZeppelin.
- Obiettivi:
  - Creare un token ERC20 **upgradeable** per Polygon Amoy testnet.
  - Usare `@openzeppelin/contracts-upgradeable` con pattern **UUPSUpgradeable** e inizializzatore.
  - Implementare `mint` e `burn` con regole di sicurezza solide.
- Regole di sicurezza:
  - `mint` consentito solo a chi possiede `MINTER_ROLE` (AccessControlUpgradeable).
  - `burn` consentito solo a `msg.sender` sul proprio saldo.
  - Uso di `AccessControlUpgradeable` per ruoli e permessi, nessuna funzione “aperta” al pubblico.
  - Emissione eventi per `Mint`, `Burn`, gestione ruoli.
- Target chain:
  - Polygon Amoy testnet (chainId 80002, RPC es. https://rpc-amoy.polygon.technology).
- Cartella di lavoro: `./solidity`

## SolidityTestAgent
- Ruolo: Scrive e mantiene i test per gli smart contract.
- Obiettivi:
  - Testare `mint`, `burn`, trasferimenti e permessi.
  - Verificare che solo gli account con `MINTER_ROLE` possano fare `mint`.
  - Verificare che `burn` non permetta di bruciare più del saldo.
  - Testare l’upgrade del contratto (deploy proxy UUPS, upgrade, stato preservato).
- Cartella di lavoro: `./solidity/test`

## FrontendAgent
- Ruolo: Implementa il frontend per la gestione del token.
- Obiettivi:
  - UI per mint (solo minter), burn, lettura balance, totalSupply e altri metodi.
  - Usare React (Vite+React) ed `ethers`.
  - Collegarsi al contratto tramite ABI e address del **proxy** su Amoy.
- Cartella di lavoro: `./frontend`

## IntegrationAgent
- Ruolo: Coordina integrazione tra smart contract e frontend.
- Obiettivi:
  - Documentare il flusso: deploy su Amoy → address proxy → configurazione frontend.
  - Mantenere aggiornati ABI e indirizzi nel frontend dopo ogni upgrade.
  - Aggiornare README con comandi per deploy, test e avvio frontend.
