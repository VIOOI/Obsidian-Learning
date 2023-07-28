Большинство строк в интерфейсах CSSOM используют `CSSOMString`тип. Каждая реализация решает определить его как [USVString](https://webidl.spec.whatwg.org/#idl-USVString)или [DOMString](https://webidl.spec.whatwg.org/#idl-DOMString):

> typedef USVString CSSOMString;

Или, альтернативно:

> typedef DOMString CSSOMString;

Разница видна только из веб-контента когда [суррогатные кодовые единицы.](https://infra.spec.whatwg.org/#surrogate) задействованы [DOMString](https://webidl.spec.whatwg.org/#idl-DOMString)сохранил бы их, тогда как [USVString](https://webidl.spec.whatwg.org/#idl-USVString)заменит их на U+FFFD REPLACEMENT CHARACTER.

Этот выбор эффективно позволяет реализациям выполнять эту замену, но не требует.

С использованием [USVString](https://webidl.spec.whatwg.org/#idl-USVString)позволяет реализовать для внутреннего использования UTF-8 для представления строк в памяти. Поскольку правильно сформированный UTF-8 специально запрещает [суррогатные](https://infra.spec.whatwg.org/#surrogate) кодовые точки, он фактически требует этой замены.

С другой стороны, реализации, которые внутренне представляют строки как 16-битные [кодовые единицы](https://infra.spec.whatwg.org/#code-unit) , могут предпочесть избежать затрат на эту замену.