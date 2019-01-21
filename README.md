# StandFordParser
Parser Usage example

先下載

CoreNLP : https://stanfordnlp.github.io/CoreNLP/

ChineseModel: http://nlp.stanford.edu/software/stanford-chinese-corenlp-2018-10-05-models.jar

接著

```
mv stanford-chinese-corenlp-2018-10-05-models.jar  StanfordCoreNLP-chinese.properties ch_oneline.txt sent.txt stanford-corenlp-full-2018-10-05
```
```
cd stanford-corenlp-full-2018-10-05
```


## CoreNLP

example ：

```
java -mx3g -cp "*" edu.stanford.nlp.pipeline.StanfordCoreNLP -props StanfordCoreNLP-chinese.properties -file ch_oneline.txt -outputFormat text
```

參數說明 ：

-mx3g ： max memory size 3GB, you can use -mx100m (max memory size 100M)

-cp : classpath, "*": all jar files in the current directory

edu.stanford.nlp.pipeline.StanfordCoreNLP: 執行的程式

-props : 設定properties，裡面有很多種設定，請見 ：https://stanfordnlp.github.io/CoreNLP/cmdline.html 與https://stanfordnlp.github.io/CoreNLP/annotators.html

-file : input file

-outputFormat : 輸出的檔案


## Parser

中文檔案先自行輸入斷詞檔，再執行。

example ：

```
java -mx3g -cp "*" edu.stanford.nlp.parser.lexparser.LexicalizedParser -maxLength 200 -sentences newline -tLPP edu.stanford.nlp.parser.lexparser.ChineseTreebankParserParams -encoding UTF-8 -writeOutputFiles -outputFilesExtension out -outputFilesDirectory ../result -outputFormat "conll2007" edu/stanford/nlp/models/lexparser/chineseFactored.ser.gz sent.txt
```

參數說明 ：

-mx3g ： max memory size 3GB

-cp : classpath, "*": all jar files in the current directory

edu.stanford.nlp.parser.lexparser.LexicalizedParser: 執行的程式

-maxLength : 句子裡的字詞長度，參數為數字 ex: 200

-sentences : 斷句的方法，可用newline, "，"等。

-tLPP edu.stanford.nlp.parser.lexparser.ChineseTreebankParserParams ： 指定 TreebankLangParserParams

-encoding UTF-8 ： 指定輸出格式

-writeOutputFiles -outputFilesDirectory ： 專門用來輸出檔案的部分

-outputFilesExtension： 輸出檔案的檔名 ex: .out

-outputFormat ： "conll2007"， "penn, typedDependenciesCollapsed" ， 可以設定許多輸出格式，輸出的結果都在同一檔案裡。輸出種類請見：https://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/trees/TreePrint.html (optionsString - Options that additionally specify how trees are to be printed (for instance, whether stemming should be done). Known options are: stem, lexicalize, markHeadNodes, xml, removeTopBracket, transChinese, includePunctuationDependencies, basicDependencies, treeDependencies, CCPropagatedDependencies, collapsedDependencies, nonCollapsedDependencies, nonCollapsedDependenciesSeparated, includeTags, conll2007.)


edu/stanford/nlp/models/lexparser/chineseFactored.ser.gz ： parser的model設定， The PCFG parsers are smaller and faster. But the Factored parser is significantly better for Chinese, and we would generally recommend its use。

最後為輸入檔：sent.txt


## Ref:
1.https://nlp.stanford edu/nlp/javadoc/javanlp/edu/stanford/nlp/parser/lexparser/package-summary.html
2.https://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/parser/lexparser/LexicalizedParser.html
3.http://puremonkey2010.blogspot.com/2012/08/stanford-parser-chinese-corpus-training.html
4.https://nlp.stanford.edu/nlp/javadoc/javanlp/edu/stanford/nlp/trees/TreePrint.html
5.https://www.cnblogs.com/stardjyeah/p/4574164.html
6.https://zhuanlan.zhihu.com/p/31765395
7.https://stanfordnlp.github.io/CoreNLP/cmdline.html
8.https://nlp.stanford.edu/software/parser-faq.html#weaker
9.https://www.cnblogs.com/stGeekpower/p/3457746.html
