Ferrando Alessandro 830405 
Borgato Jacopo 866305

Il seguente README riguarda l’implementazione in Common Lisp di un parser per delle URI semplificate, ovvero una libreria che le rappresenti internamente partendo dalla loro rappresentazione come stringhe.

NB. La sintassi delle stringhe URI utilizzata in questo progetto è la seguente: 
- URI ::= URI1 | URI2
- URI1 ::= scheme ':' authorithy [‘/‘ [path]] [‘?’ query] [‘#’ fragment]
        |  scheme ‘:’ [‘/’] [path] [‘?’ query] [‘#’ fragment]
- URI2 ::= scheme ‘:’ scheme-syntax
Dove scheme, authority, path, query, fragment, scheme-syntax sono definiti nel testo del progetto.


Nel programma sono state definite le seguenti funzioni principali:

;; uri-parse: funzione prinicpale la quale trasforma una stringa in input nella struttura uri-struct
;
;; uri-scheme: data in input una uri-struct ritorna lo scheme
;
;; uri-userinfo: data in input una uri-struct ritorna l'userinfo, nil se non esiste
;
;; uri-host: data in input una uri-struct ritorna l'host, nil se non esiste
;
;; uri-port: data in input una uri-struct ritorna la porta, 80 di default
;
;; uri-path: data in input una uri-struct ritorna il path, nil se non esiste
;
;; uri-query: data in input una uri-struct ritorna la query, nil se non esiste
;
;; uri-fragment: data in input una uri-struct ritorna il fragment, nil se non esiste
;
;; uri-display: data in input una uri-struct stampa a schermo i vari campi


Altre funzioni invece sono state definite per il funzionamento:
;; after-parse: data in unput una uri-struct controlla se sia valida
;
;; check-host: dato in input un host controlla che sia valido
;
;; consume-list: date due liste in input risorna la lista non in comune
;
;; is-alpha: dato un carattere in input controlla che sia alfabetico
;
;; check-zos-path: dato un path zos in input controlla che sia valido chiamando
					check-zos-path-id44 e check-zos-path-id8
;
;; check-zos-path-id44: dato un path zos in input controlla se la parte id44 sia valida
;
;; check-zos-path-id8: dato un path zos in input controlla se la parte id8 sia valida
;
;; get-autority: questa funzione serve per facilitare il parsing dell'auotority.
					controlla se lo scheme sia speciale e ritorna una lista contenente l'autority
;
;; get-autority-mailto: nel caso lo scheme sia speciale "mailto" ritorna una lista contenente i carattery dell'autority
;
;; get-autority-nft: ritorna una lista contenente l'autority nel caso lo scheme sia del tipo "news" oppure "fax" oppure "tel
;
;; get-autority-gen: funzione generale che ritorna l'autority nel caso lo scheme non sia speciale o nel caso sia zos
;
;; mini-check-gen-aut: controlla che l'autority non sia nulla nel caso generale o zos
;
;; get-after-autority: data in input una lista URI ritorna una lista contenente i caratteri dopo l'autority
;
;; parse-uri-scheme: data in input una lista URI ritorna lo scheme
;
;; parse-uri-userinfo: data in input una lista contenente i caratteri dell'autority ritorna l'userinfo controllando se lo scheme sia generale o speciale
;
;; parse-uri-userinfo-ft: data in input una lista ritorna l'userinfo nel caso degli scheme speciali fax e tel
;
;; parse-uri-userinfo-mailto:data in input una lista ritorna l'userinfo nel caso dello scheme speciale mailto
;
;; parse-uri-userinfo-gen: data in input una lista ritorna l'userinfo nel caso di uno scheme generale o dello scheme zos
;
;; get-after-user: data in input una lista e una uri-struct controlla di che tipo e' lo scheme e ritorna la lista di caratteri dell'uri dopo l'user
;
;; get-after-user-mailto: ritorna una list adi caratteri dopo l'userinfo nel caso lo scheme sia del tipo mailto
;
;; get-after-user-gen: ritorna una list adi caratteri dopo l'userinfo nel caso generale
;
;; parse-uri-host: data in input una lista contenente i caratteri dell'autority ritorna l'host controllando se lo scheme sia generale o speciale
;
;; parse-uri-host-mn: data in input una lista ritorna l'host nel caso degli scheme speciali mail e news
;
;; parse-uri-host-gen: data in input una lista ritorna l'host nel caso generale o nel caso dello scheme zos
;
;; parse-uri-port: data in input una porta imposta di default la porta 80 e se la porta esiste allora ritorna il valore della porta
;
;; parse-uri-port-gen: ritorna il valore della porta nel caso generale
;
;; parse-uri-path: data in input una lista ritorna una lista contenente i caratteri del path dell'URI
;
;; parse-uri-query: data in input una lista ritorna una lista contenente i caratteri della query dell'URI
;
;; parse-uri-fragment: data in input una lista ritorna una lista contenente i caratteri del fragment dell'URI
;
;; void-to-nil: data in input una stringa controlla se sia vuota e nel caso ritona nil
;
;; port-to-nil: data in input una stringa se vuota ritorna nil altrimenti il valore numerico
