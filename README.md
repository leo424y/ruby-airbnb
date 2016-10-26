# Ruby 代碼風格指南

這是 Airbnb 的 Ruby 代碼風格指南。

這份指南的靈感來自於 [Github 的指南](https://web.archive.org/web/20160410033955/https://github.com/styleguide/ruby) 和 [Bozhidar Batsov 的指南][bbatsov-ruby]。

Airbnb 也在維護 [JavaScript 風格指南][airbnb-javascript]。

## 內容表 (Table of Contents)
  1. [空格 (Whitespace)](#空格-whitespace)
    1. [縮進 (Indentation)](#縮進-indentation)
    1. [行內 (Inline)](#行內-inline)
    1. [換行 (Newlines)](#換行-newlines)
  1. [行寬 (Line Length)](#行寬-line-length)
  1. [註釋 (Commenting)](#註釋-commenting)
    1. [文件級/類級 註釋 (File/class-level comments)](#文件類-級別的註釋-fileclass-level-comments)
    1. [函數註釋 (Function comments)](#函數註釋-function-comments)
    1. [塊級和行內註釋 (Block and inline comments)](#塊級和行內註釋-block-and-inline-comments)
    1. [標點符號, 拼寫和語法 (Punctuation, spelling, and grammar)](#標點符號-拼寫和語法-punctuation-spelling-and-grammar)
    1. [待辦註釋 (TODO comments)](#待辦註釋-todo-comments)
    1. [註釋掉的代碼 (Commented-out code)](#註釋掉的代碼-commented-out-code)
  1. [方法 (Methods)](#方法-methods)
    1. [方法定義 (Method definitions)](#方法定義-method-definitions)
    1. [方法調用 (Method calls)](#方法調用-method-calls)
  1. [條件表達式 (Conditional Expressions)](#條件表達式-conditional-expressions)
    1. [關鍵字 (Conditional keywords)](#關鍵字-conditional-keywords)
    1. [三元操作符 (Ternary operator)](#三元操作符-ternary-operator)
  1. [語法 (Syntax)](#語法-syntax)
  1. [命名 (Naming)](#命名-naming)
  1. [類 (Classes)](#類-classes)
  1. [異常 (Exceptions)](#異常-exceptions)
  1. [集合 (Collections)](#集合-collections)
  1. [字符串 (Strings)](#字符串-strings)
  1. [正則表達式 (Regular Expressions)](#正則表達式-regular-expressions)
  1. [百分比字面量 (Percent Literals)](#百分比字面量-percent-literals)
  1. [Rails](#rails)
    1. [範圍 (Scopes)](#範圍-scopes)
  1. [保持一致 (Be Consistent)](#保持一致-be-consistent)

## 空格 (Whitespace)

### 縮進 (Indentation)

* <a name="default-indentation"></a>始終用 2 個空格做縮進。<sup>[[link](#default-indentation)]</sup>

* <a name="indent-when-as-case"></a> `when` 的縮進和 `case` 一致。
    <sup>[[link](#indent-when-as-case)]</sup>

    ```ruby
    case
    when song.name == 'Misty'
      puts 'Not again!'
    when song.duration > 120
      puts 'Too long!'
    when Time.now.hour > 21
      puts "It's too late"
    else
      song.play
    end

    kind = case year
           when 1850..1889 then 'Blues'
           when 1890..1909 then 'Ragtime'
           when 1910..1929 then 'New Orleans Jazz'
           when 1930..1939 then 'Swing'
           when 1940..1950 then 'Bebop'
           else 'Jazz'
           end
    ```

* <a name="align-function-params"></a>函數的參數要麼全部在同一行，如果參數要分成多行，則每行一個參數， 相同縮進。<sup>[[link](#align-function-params)]</sup>

    ```ruby
    # 錯誤
    def self.create_translation(phrase_id, phrase_key, target_locale,
                                value, user_id, do_xss_check, allow_verification)
      ...
    end

    # 正確
    def self.create_translation(phrase_id,
                                phrase_key,
                                target_locale,
                                value,
                                user_id,
                                do_xss_check,
                                allow_verification)
      ...
    end

    # 正確
    def self.create_translation(
      phrase_id,
      phrase_key,
      target_locale,
      value,
      user_id,
      do_xss_check,
      allow_verification
    )
      ...
    end
    ```

* <a name="indent-multi-line-bool"></a>多行的布爾表達式，下一行縮進一下。<sup>[[link](#indent-multi-line-bool)]</sup>

    ```ruby
    # 錯誤
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
      is_in_program?(user) &&
      program_not_expired
    end

    # 正確
    def is_eligible?(user)
      Trebuchet.current.launch?(ProgramEligibilityHelper::PROGRAM_TREBUCHET_FLAG) &&
        is_in_program?(user) &&
        program_not_expired
    end
    ```

### 行內 (Inline)

* <a name="trailing-whitespace"></a>行末不要留空格。
    <sup>[[link](#trailing-whitespace)]</sup>

* <a name="space-before-comments"></a>寫行內註釋的時候，在代碼和註釋之間放 1 個空格。
    <sup>[[link](#space-before-comments)]</sup>

    ```ruby
    # 錯誤
    result = func(a, b)# we might want to change b to c

    # 正確
    result = func(a, b) # we might want to change b to c
    ```

* <a name="spaces-operators"></a>操作符兩邊放一個空格；逗號，冒號，分號後面都放一個空格；左大括號 `{` 兩邊放空格，右大括號 `}` 左邊放空格。
    <sup>[[link](#spaces-operators)]</sup>

    ```ruby
    sum = 1 + 2
    a, b = 1, 2
    1 > 2 ? true : false; puts 'Hi'
    [1, 2, 3].each { |e| puts e }
    ```

* <a name="no-space-before-commas"></a>逗號前面永遠不要放空格
    <sup>[[link](#no-space-before-commas)]</sup>

    ```ruby
    result = func(a, b)
    ```

* <a name="spaces-block-params"></a>block 語法裡，|   | 內部的兩邊不應該帶多餘的空格，參數之間應該有1個空格，|   | 後面應該有一個空格
    <sup>[[link](#spaces-block-params")]</sup>

    ```ruby
    # 錯誤
    {}.each { | x,  y |puts x }

    # 正確
    {}.each { |x, y| puts x }
    ```

* <a name="no-space-after-!"></a>感嘆號和參數間不要留空格，下面是個正確的例子。<sup>[[link](#no-space-after-!)]</sup>

    ```ruby
    !something
    ```

* <a name="no-spaces-braces"></a> `(`, `[` 後面不要有空格
    `]`, `)` 前面不要有空格
    <sup>[[link](#no-spaces-braces)]</sup>

    ```ruby
    some(arg).other
    [1, 2, 3].length
    ```

* <a name="no-spaces-string-interpolation"></a>
    字符串插值時候忽略空格。<sup>[[link](#no-spaces-string-interpolation)]</sup>

    ```ruby
    # 錯誤
    var = "This #{ foobar } is interpolated."

    # 正確
    var = "This #{foobar} is interpolated."
    ```

* <a name="no-spaces-range-literals"></a>當表達範圍時，不要寫額外的空格。<sup>[[link](#no-spaces-range-literals)]</sup>

    ```ruby
    # 錯誤
    (0 ... coll).each do |item|

    # 正確
    (0...coll).each do |item|
    ```

### 換行 (Newlines)

* <a name="multiline-if-newline"></a>if 條件保持相同縮進，方便識別哪些是條件，哪些是內容。
    <sup>[[link](#multiline-if-newline)]</sup>

    ```ruby
    if @reservation_alteration.checkin == @reservation.start_date &&
       @reservation_alteration.checkout == (@reservation.start_date + @reservation.nights)

      redirect_to_alteration @reservation_alteration
    end
    ```

* <a name="newline-after-conditional"></a>條件語句，塊，case 語句，等等東西后面換一行， 例子如下。<sup>[[link](#newline-after-conditional)]</sup>

    ```ruby
    if robot.is_awesome?
      send_robot_present
    end

    robot.add_trait(:human_like_intelligence)
    ```

* <a name="newline-different-indent"></a>不同縮進的代碼之間無需空行 (比如 class 或 module 和內容之間)。
    <sup>[[link](#newline-different-indent)]</sup>

    ```ruby
    # 錯誤
    class Foo

      def bar
        # body omitted
      end

    end

    # 正確
    class Foo
      def bar
        # body omitted
      end
    end
    ```

* <a name="newline-between-methods"></a>方法之間 1 個空行就好。<sup>[[link](#newline-between-methods)]</sup>

    ```ruby
    def a
    end

    def b
    end
    ```

* <a name="method-def-empty-lines"></a>1 個空行隔開類似的邏輯。
    <sup>[[link](#method-def-empty-lines)]</sup>

    ```ruby
    def transformorize_car
      car = manufacture(options)
      t = transformer(robot, disguise)

      car.after_market_mod!
      t.transform(car)
      car.assign_cool_name!

      fleet.add(car)
      car
    end
    ```

* <a name="trailing-newline"></a>文件末尾只放一個空行。
    <sup>[[link](#trailing-newline)]</sup>

## 行寬 (Line Length)

* 把每一行控制在可讀寬度內，
  除非有特別理由, 每一行應小於 100 個字符
  ([rationale](./rationales.md#line-length))<sup>
  [[link](#line-length)]</sup>

## 註釋 (Commenting)

> 雖然寫註釋很痛苦, 但是對於保持代碼可讀非常重要
> 下面的規則描述了你應該怎麼寫註釋, 以及寫在哪裡。
> 但是記住：註釋雖然非常重要, 但是最好的註釋是代碼本身。
> 直觀的變量名本身就是註釋， 比起起一個奇怪的名字，然後用註釋解釋要好得多

> 當寫註釋時，為你的觀眾去寫：下一個貢獻者需要理解你的代碼。
> 請慷慨一些 - 下一個可能就是你自己！

&mdash;[Google C++ 風格指南][google-c++]

這一部分的指南從 Google
[C++][google-c++-comments] 和 [Python][google-python-comments] 風格指南那邊借鑑了很多。

### 文件/類 級別的註釋 (File/class-level comments)

每個類的定義都應該帶些註釋， 說明它是幹什麼的, 以及怎麼用它。

如果文件裡沒有任何 class， 或者多於一個 class， 頂部應該有註釋說明裡面是什麼。

```ruby
# Automatic conversion of one locale to another where it is possible, like
# American to British English.
module Translation
  # Class for converting between text between similar locales.
  # Right now only conversion between American English -> British, Canadian,
  # Australian, New Zealand variations is provided.
  class PrimAndProper
    def initialize
      @converters = { :en => { :"en-AU" => AmericanToAustralian.new,
                               :"en-CA" => AmericanToCanadian.new,
                               :"en-GB" => AmericanToBritish.new,
                               :"en-NZ" => AmericanToKiwi.new,
                             } }
    end

  ...

  # Applies transforms to American English that are common to
  # variants of all other English colonies.
  class AmericanToColonial
    ...
  end

  # Converts American to British English.
  # In addition to general Colonial English variations, changes "apartment"
  # to "flat".
  class AmericanToBritish < AmericanToColonial
    ...
  end
```

所有文件，包括數據和配置文件，都應該有文件級別(file-level)的註釋。

```ruby
# List of American-to-British spelling variants.
#
# This list is made with
# lib/tasks/list_american_to_british_spelling_variants.rake.
#
# It contains words with general spelling variation patterns:
#   [trave]led/lled, [real]ize/ise, [flav]or/our, [cent]er/re, plus
# and these extras:
#   learned/learnt, practices/practises, airplane/aeroplane, ...

sectarianizes: sectarianises
neutralization: neutralisation
...
```

### 函數註釋 (Function comments)

函數聲明的前面都應該有註釋，描述函數是做什麼的，以及怎麼用。
這些註釋應該是 描述性的(descriptive) 比如 ("Opens the file")
而不是 命令式的(imperative) 比如 ("Open the file")；
註釋描述這個函數，而不是告訴這個函數應該做什麼。
總的來說，函數前面的註釋並不負責解釋函數是怎麼做到它提供的功能的。
解釋功能怎麼實現的註釋，應該零散的分佈在函數內部的註釋裡。

每個函數都應該提到輸入和輸出是什麼，除非碰到以下情況：

* 不是外部可見的函數 (not externally visible)
* 非常短 (very short)
* 很明顯 (obvious)

你喜歡什麼格式都行。在 Ruby 裡兩種常見的格式是 [TomDoc](http://tomdoc.org/) 和 [YARD](http://rubydoc.info/docs/yard/file/docs/GettingStarted.md)。
你也可以直接簡潔明瞭的寫出來，比如這樣：

```ruby
# Returns the fallback locales for the_locale.
# If opts[:exclude_default] is set, the default locale, which is otherwise
# always the last one in the returned list, will be excluded.
#
# For example:
#   fallbacks_for(:"pt-BR")
#     => [:"pt-BR", :pt, :en]
#   fallbacks_for(:"pt-BR", :exclude_default => true)
#     => [:"pt-BR", :pt]
def fallbacks_for(the_locale, opts = {})
  ...
end
```

### 塊級和行內註釋 (Block and inline comments)

這個部分有點小麻煩. 如果你下次 code review 需要解釋這些代碼的話， 你現在就應該寫註釋。
複雜的操作應該把註釋寫在前面。
單行的不太容易理解的代碼, 註釋應該寫在代碼後面。

```ruby
def fallbacks_for(the_locale, opts = {})
  # dup() to produce an array that we can mutate.
  ret = @fallbacks[the_locale].dup

  # We make two assumptions here:
  # 1) There is only one default locale (that is, it has no less-specific
  #    children).
  # 2) The default locale is just a language. (Like :en, and not :"en-US".)
  if opts[:exclude_default] &&
      ret.last == default_locale &&
      ret.last != language_from_locale(the_locale)
    ret.pop
  end

  ret
end
```
在另一方面，永遠不要在註釋裡描述代碼。你要假設讀代碼的人對這門語言的瞭解比你知道的多。

<a name="no-block-comments"></a>相關的一個事兒：不要用塊級註釋，他們前面沒有空格，不方便一眼認出來是註釋。
  <sup>[[link](#no-block-comments)]</sup>

  ```ruby
  # 錯誤
  =begin
  comment line
  another comment line
  =end

  # 正確
  # comment line
  # another comment line
  ```

### 標點符號, 拼寫和語法 (Punctuation, spelling, and grammar)

要注意註釋裡的標點符號, 拼寫和語法；
註釋寫得好讀起來也容易。

註釋應該和敘述文 (narrative text) 一樣易讀 (readable)，
有著正確的大小寫和標點符號。 在很多情況下。 完整的句子比句子碎片容易讀得多。
短的註釋， 比如跟在代碼後面的， 可以不那麼正式， 但風格應該一致。

雖然在提交代碼時, 別人指出你在應該用分號的地方用了逗號, 這種小事蠻折磨人的.
但重要的是源代碼應該保持高度的清晰和可讀. 正確的標點符號, 拼寫, 和語法非常重要.


### 待辦註釋 (TODO comments)

當代碼是臨時解決方案，夠用但是並不完美時，用 TODO 註釋。

TODO 應該全大寫, 然後是寫這個註釋的人名, 用圓括號括起來, 冒號可寫可不寫。
然後後面是解釋需要做什麼，統一 TODO 註釋樣式的目的是方便搜索。
括號裡的人名不代表這個人負責解決這個問題, 只是說這個人知道這裡要解決什麼問題.
每次你寫 TODO 註釋的時候加上你的名字。

```ruby
  # 錯誤
  # TODO(RS): Use proper namespacing for this constant.

  # 錯誤
  # TODO(drumm3rz4lyfe): Use proper namespacing for this constant.

  # 正確
  # TODO(Ringo Starr): Use proper namespacing for this constant.
```

### 註釋掉的代碼 (Commented-out code)

* <a name="commented-code"></a>註釋掉的代碼就不要留在代碼庫裡了。
    <sup>[[link](#commented-code)]</sup>

## 方法 (Methods)

### 方法定義 (Method definitions)

* <a name="method-def-parens"></a>函數要接參數的時候就用括號, 不用參數時就不用寫括號了。 下面是正確的例子.<sup>[[link](#method-def-parens)]</sup>

     ```ruby
     def some_method
       # body omitted
     end

     def some_method_with_parameters(arg1, arg2)
       # body omitted
     end
     ```

* <a name="no-default-args"></a>不要用默認參數，用一個選項 hash 來做這個事。<sup>[[link](#no-default-args)]</sup>

    ```ruby
    # 錯誤
    def obliterate(things, gently = true, except = [], at = Time.now)
      ...
    end

    # 正確
    def obliterate(things, options = {})
      default_options = {
        :gently => true, # obliterate with soft-delete
        :except => [], # skip obliterating these things
        :at => Time.now, # don't obliterate them until later
      }
      options.reverse_merge!(default_options)

      ...
    end
    ```

* <a name="no-single-line-methods"></a> 避免定義單行函數，雖然有些人喜歡這樣寫，但是這樣容易引起一些奇怪的問題
    <sup>[[link](#no-single-line-methods)]</sup>

    ```ruby
    # 錯誤
    def too_much; something; something_else; end

    # 正確
    def some_method
      # body
    end
    ```

### 方法調用 (Method calls)

應該用 **圓括號** 的情況：

* <a name="returns-val-parens"></a>如果方法會返回值。
    <sup>[[link](#returns-val-parens)]</sup>

    ```ruby
    # 錯誤
    @current_user = User.find_by_id 1964192

    # 正確
    @current_user = User.find_by_id(1964192)
    ```

* <a name="first-arg-parens"></a>如果第一個參數需要圓括號。<sup>[[link](#first-arg-parens)]</sup>

    ```ruby
    # 錯誤
    put! (x + y) % len, value

    # 正確
    put!((x + y) % len, value)
    ```

* <a name="space-method-call"></a>方法名和左括號之間永遠不要放空格。<sup>[[link](#space-method-call)]</sup>

    ```ruby
    # 錯誤
    f (3 + 2) + 1

    # 正確
    f(3 + 2) + 1
    ```

* <a name="no-args-parens"></a> 對於不用接收參數的方法， **忽略圓括號** 。<sup>[[link](#no-args-parens)]</sup>

    ```ruby
    # 錯誤
    nil?()

    # 正確
    nil?
    ```

* <a name="no-return-parens"></a>如果方法不返回值 (或者我們不關心返回值)，那麼帶不帶括號都行。
    (如果參數會導致代碼多於一行， 建議加個括號比較有可讀性)
    <sup>[[link](#no-return-parens)]</sup>

    ```ruby
    # okay
    render(:partial => 'foo')

    # okay
    render :partial => 'foo'
    ```

不論什麼情況:

* <a name="options-no-braces"></a>如果一個方法的最後一個參數接收 hash， 那麼不需要 `{` `}` 。
    <sup>[[link](#options-no-braces)]</sup>

    ```ruby
    # 錯誤
    get '/v1/reservations', { :id => 54875 }

    # 正確
    get '/v1/reservations', :id => 54875
    ```

## 條件表達式 (Conditional Expressions)

### 關鍵字 (Conditional keywords)

* <a name="multiline-if-then"></a>永遠不要把 `then` 和多行的 `if/unless` 搭配使用。
    <sup>[[link](#multiline-if-then)]</sup>

    ```ruby
    # 錯誤
    if some_condition then
      ...
    end

    # 正確
    if some_condition
      ...
    end
    ```

* <a name="multiline-while-until"></a> `do` 不要和多行的 `while` 或 `until`搭配使用。<sup>[[link](#multiline-while-until)]</sup>

    ```ruby
    # 錯誤
    while x > 5 do
      ...
    end

    until x > 5 do
      ...
    end

    # 正確
    while x > 5
      ...
    end

    until x > 5
      ...
    end
    ```

* <a name="no-and-or"></a>`and`, `or`， 和`not` 關鍵詞禁用。 因為不值得。 總是用 `&&`， `||`， 和 `!` 來代替。
    <sup>[[link](#no-and-or)]</sup>

* <a name="only-simple-if-unless"></a>適合用 `if/unless` 的情況： 內容簡單， 條件簡單， 整個東西能塞進一行。
    不然的話， 不要用 `if/unless`。
    <sup>[[link](#only-simple-if-unless)]</sup>

    ```ruby
    # 錯誤 - 一行塞不下
    add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page]) if request_opts[:trebuchet_experiments_on_page] && !request_opts[:trebuchet_experiments_on_page].empty?

    # 還行
    if request_opts[:trebuchet_experiments_on_page] &&
         !request_opts[:trebuchet_experiments_on_page].empty?

      add_trebuchet_experiments_on_page(request_opts[:trebuchet_experiments_on_page])
    end

    # 錯誤 - 這個很複雜,需要寫成多行,而且需要註釋
    parts[i] = part.to_i(INTEGER_BASE) if !part.nil? && [0, 2, 3].include?(i)

    # 還行
    return if reconciled?
    ```

* <a name="no-unless-with-else"></a>不要把 `unless` 和 `else` 搭配使用。<sup>[[link](#no-unless-with-else)]</sup>

    ```ruby
    # 錯誤
    unless success?
      puts 'failure'
    else
      puts 'success'
    end

    # 正確
    if success?
      puts 'success'
    else
      puts 'failure'
    end
    ```

* <a name="unless-with-multiple-conditions"></a>避免用多個條件的 `unless`
    。<sup>[[link](#unless-with-multiple-conditions)]</sup>

    ```ruby
      # 錯誤
      unless foo? && bar?
        ...
      end

      # 還行
      if !(foo? && bar?)
        ...
      end
    ```

* <a name="parens-around-conditions"></a>條件語句 `if/unless/while` 不需要圓括號。
    <sup>[[link](#parens-around-conditions)]</sup>

    ```ruby
    # 錯誤
    if (x > 10)
      ...
    end

    # 正確
    if x > 10
      ...
    end

    ```

### 三元操作符 (Ternary operator)

* <a name="avoid-complex-ternary"></a>避免使用三元操作符 (`?:`)，如果不用三元操作符會變得很囉嗦才用。
    對於單行的條件, 用三元操作符(`?:`) 而不是 `if/then/else/end`.<sup>[[link](#avoid-complex-ternary)]</sup>

    ```ruby
    # 錯誤
    result = if some_condition then something else something_else end

    # 正確
    result = some_condition ? something : something_else
    ```

* <a name="no-nested-ternaries"></a>不要嵌套使用三元操作符，換成
    `if/else`.<sup>[[link](#no-nested-ternaries)]</sup>

    ```ruby
    # 錯誤
    some_condition ? (nested_condition ? nested_something : nested_something_else) : something_else

    # 正確
    if some_condition
      nested_condition ? nested_something : nested_something_else
    else
      something_else
    end
    ```

* <a name="single-condition-ternary"></a>避免多條件三元操作符。最好判斷一個條件。
    <sup>[[link](#single-condition-ternary)]</sup>

* <a name="no-multiline-ternaries"></a>避免拆成多行的 `?:` (三元操作符), 用 `if/then/else/end` 就好了。
    <sup>[[link](#no-multiline-ternaries)]</sup>

    ```ruby
    # 錯誤
    some_really_long_condition_that_might_make_you_want_to_split_lines ?
      something : something_else

    # 正確
    if some_really_long_condition_that_might_make_you_want_to_split_lines
      something
    else
      something_else
    end
    ```

## 語法 (Syntax)

* <a name="no-for"></a>永遠不要用 `for`，除非有非常特殊的理由。
    絕大部分情況都應該用 `each`。 `for` 是用 `each` 實現的(所以你間接加了一層)，
    但區別是 - `for` 不會有新 scope (不像 `each`) 裡面定義的變量外面可見。<sup>[[link](#no-for)]</sup>

    ```ruby
    arr = [1, 2, 3]

    # 錯誤
    for elem in arr do
      puts elem
    end

    # 正確
    arr.each { |elem| puts elem }
    ```

* <a name="single-line-blocks"></a>
    單行的情況下, 儘量用 `{...}` 而不是 `do...end`。
    多行的情況下避免用 `{...}`.
    對於 "control flow" 和 "方法定義"(舉例: 在 Rakefiles 和某些 DSLs 裡) 總是用 `do...end`。
    方法連用(chaining)時 避免使用 `do...end` 。<sup>[[link](#single-line-blocks)]</sup>

    ```ruby
    names = ["Bozhidar", "Steve", "Sarah"]

    # 正確
    names.each { |name| puts name }

    # 錯誤
    names.each do |name| puts name end

    # 正確
    names.each do |name|
      puts name
      puts 'yay!'
    end

    # 錯誤
    names.each { |name|
      puts name
      puts 'yay!'
    }

    # 正確
    names.select { |name| name.start_with?("S") }.map { |name| name.upcase }

    # 錯誤
    names.select do |name|
      name.start_with?("S")
    end.map { |name| name.upcase }
    ```

    有些人會說多行連用(chaining) 用
    `{...}` 符號 其實也沒那麼難看, 但他們應該問問自己這代碼真的可讀嗎, 而且 block 裡的內容是否可以抽出來弄好看些.

* <a name="self-assignment"></a>儘可能用短的自賦值操作符 (self assignment operators)。<sup>[[link](#self-assignment)]</sup>

    ```ruby
    # 錯誤
    x = x + y
    x = x * y
    x = x**y
    x = x / y
    x = x || y
    x = x && y

    # 正確
    x += y
    x *= y
    x **= y
    x /= y
    x ||= y
    x &&= y
    ```

* <a name="semicolons"></a>避免用分號。 除非是單行 class 定義的情況下。 而且當使用分號時， 分號前面不應該有空格。<sup>[[link](#semicolons)]</sup>

    ```ruby
    # 錯誤
    puts 'foobar'; # 多餘的分號
    puts 'foo'; puts 'bar' # 兩個表達式放到一行

    # 正確
    puts 'foobar'

    puts 'foo'
    puts 'bar'

    puts 'foo', 'bar' # this applies to puts in particular
    ```

* <a name="colon-use"></a>:: 的使用場景是引用常量，(比如
    classes 和 modules 裡的常量) 以及調用構造函數 (比如 Array() 或者 Nokogiri::HTML())。
    普通方法調用就不要使用 :: 了。<sup>[[link](#colon-use)]</sup>

    ```ruby
    # 錯誤
    SomeClass::some_method
    some_object::some_method

    # 正確
    SomeClass.some_method
    some_object.some_method
    SomeModule::SomeClass::SOME_CONST
    SomeModule::SomeClass()
    ```

* <a name="redundant-return"></a>儘量避免用 `return`。
    <sup>[[link](#redundant-return)]</sup>

    ```ruby
    # 錯誤
    def some_method(some_arr)
      return some_arr.size
    end

    # 正確
    def some_method(some_arr)
      some_arr.size
    end
    ```

* <a name="assignment-in-conditionals"></a>條件語句裡不要用返回值<sup>[[link](#assignment-in-conditionals)]</sup>

    ```ruby
    # 錯誤 - shows intended use of assignment
    if (v = array.grep(/foo/))
      ...
    end

    # 錯誤
    if v = array.grep(/foo/)
      ...
    end

    # 正確
    v = array.grep(/foo/)
    if v
      ...
    end

    ```

* <a name="double-pipe-for-uninit"></a>請隨意用 `||=` 來初始化變量。
    <sup>[[link](#double-pipe-for-uninit)]</sup>

    ```ruby
    # 把 name 賦值為 Bozhidar, 僅當 name 是 nil 或者 false 時
    name ||= 'Bozhidar'
    ```

* <a name="no-double-pipes-for-bools"></a>不要用 `||=` 來初始化布爾變量。
    (想象下如果值剛好是 `false` 會咋樣.)<sup>[[link](#no-double-pipes-for-bools)]</sup>

    ```ruby
    # 錯誤 - would set enabled to true even if it was false
    enabled ||= true

    # 正確
    enabled = true if enabled.nil?
    ```

* <a name="lambda-calls"></a>當調用 lambdas 時，明確使用 `.call`。
    <sup>[[link](#lambda-calls)]</sup>

    ```ruby
    # 錯誤
    lambda.(x, y)

    # 正確
    lambda.call(x, y)
    ```

* <a name="no-cryptic-perl"></a>避免使用 Perl 風格的特殊變量名
    ( 比如 `$0-9`, `$`, 等等. ). 因為看起來蠻神祕的. 建議只在單行裡使用。建議用長名字， 比如 `$PROGRAM_NAME`.<sup>[[link](#no-cryptic-perl)]</sup>

* <a name="single-action-blocks"></a>當一個方法塊只需要 1 個參數，而且方法體也只是讀一個屬性， 或者無參數的調用一樣方法，這種情況下用 `&:` .
    <sup>[[link](#single-action-blocks)]</sup>

    ```ruby
    # 錯誤
    bluths.map { |bluth| bluth.occupation }
    bluths.select { |bluth| bluth.blue_self? }

    # 正確
    bluths.map(&:occupation)
    bluths.select(&:blue_self?)
    ```

* <a name="redundant-self"></a>當調用當前實例的某個方法時， 儘量用 `some_method` 而不是 `self.some_method`。<sup>[[link](#redundant-self)]</sup>

    ```ruby
    # 錯誤
    def end_date
      self.start_date + self.nights
    end

    # 正確
    def end_date
      start_date + nights
    end
    ```

    在下面 3 種常見情況裡, 需要用, 而且應該用`self.`:

    1. 當定義一個類方法時: `def self.some_method`.
    2. 當調用一個賦值方法 (assignment method) 時,*左手邊* 應該用 self, 比如當 self 是 ActiveRecord  模型然後你需要賦值一個屬性: `self.guest = user`.
    3. 指向 (Referencing) 當前實例的類: `self.class`.

## 命名 (Naming)

* <a name="snake-case"></a>用 蛇命名法 (`snake_case`) 來命名 methods 和 variables。
    <sup>[[link](#snake-case)]</sup>

* <a name="camel-case"></a>用 駝峰命名法(`CamelCase`) 命名 class 和 module。 (縮寫詞如 HTTP, RFC, XML 全部大寫)
    <sup>[[link](#camel-case)]</sup>

* <a name="screaming-snake-case"></a>用尖叫蛇命名法 (`SCREAMING_SNAKE_CASE`) 來命名常量。<sup>[[link](#screaming-snake-case)]</sup>

* <a name="predicate-method-names"></a>斷定方法的名字 (predicate methods) (意思是那些返回布爾值的方法) 應該以問號結尾。
    (比如 `Array#empty?`)。<sup>[[link](#predicate-method-names)]</sup>

* <a name="bang-methods"></a>有一定 "潛在危險" 的方法
    (意思就是那些. 會修改 `self` 的方法, 或者原地修改參數的方法, 或者帶有 `exit!` 的方法, 等等) 應該以感嘆號結尾. 這種危險方法應該僅當同名的不危險方法存在之後, 才存在. ([More on this][ruby-naming-bang].)
    <sup>[[link](#bang-methods)]</sup>

* <a name="throwaway-variables"></a>把不用的變量名命名為 `_`.
    <sup>[[link](#throwaway-variables)]</sup>

    ```ruby
    payment, _ = Payment.complete_paypal_payment!(params[:token],
                                                  native_currency,
                                                  created_at)
    ```

## 類 (Classes)

* <a name="avoid-class-variables"></a>避免使用類變量(`@@`)，
    因為在繼承的時候它們會有 "淘氣" 的行為。
    <sup>[[link](#avoid-class-variables)]</sup>

    ```ruby
    class Parent
      @@class_var = 'parent'

      def self.print_class_var
        puts @@class_var
      end
    end

    class Child < Parent
      @@class_var = 'child'
    end

    Parent.print_class_var # => 會輸出"child"
    ```

  你可以看到在這個類的繼承層級了，所有的類都共享一個類變量。 儘量使用實例變量而不是類變量。

* <a name="singleton-methods"></a>用 `def self.method` 來定義單例方法(singleton
    methods). 這樣在需要改類名的時候更方便.
    <sup>[[link](#singleton-methods)]</sup>

    ```ruby
    class TestClass
      # 錯誤
      def TestClass.some_method
        ...
      end

      # 正確
      def self.some_other_method
        ...
      end
    ```
* <a name="no-class-self"></a>除非必要，避免寫 `class << self`，
   必要的情況比如 single accessors 和 aliased attributes。
    <sup>[[link](#no-class-self)]</sup>

    ```ruby
    class TestClass
      # 錯誤
      class << self
        def first_method
          ...
        end

        def second_method_etc
          ...
        end
      end

      # 正確
      class << self
        attr_accessor :per_page
        alias_method :nwo, :find_by_name_with_owner
      end

      def self.first_method
        ...
      end

      def self.second_method_etc
        ...
      end
    end
    ```

* <a name="access-modifiers"></a> `public`, `protected`,  `private` 它們和方法定義保持相同縮進。 並且上下各留一個空行。<sup>[[link](#access-modifiers)]</sup>

    ```ruby
    class SomeClass
      def public_method
        # ...
      end

      private

      def private_method
        # ...
      end
    end
    ```

## 異常 (Exceptions)

* <a name="exception-flow-control"></a>不要把異常用於控制流裡 (flow of control)
    <sup>[[link](#exception-flow-control)]</sup>

    ```ruby
    # 錯誤
    begin
      n / d
    rescue ZeroDivisionError
      puts "Cannot divide by 0!"
    end

    # 正確
    if d.zero?
      puts "Cannot divide by 0!"
    else
      n / d
    end
    ```

* <a name="dont-rescue-exception"></a>避免捕捉 `Exception` 這個大類的異常
    <sup>[[link](#dont-rescue-exception)]</sup>

    ```ruby
    # 錯誤
    begin
      # an exception occurs here
    rescue Exception
      # exception handling
    end

    # 正確
    begin
      # an exception occurs here
    rescue StandardError
      # exception handling
    end

    # 可以接受
    begin
      # an exception occurs here
    rescue
      # exception handling
    end
    ```

* <a name="redundant-exception"></a>傳 2 個參數調 raise 異常時不要明確指明`RuntimeError`。儘量用 error 子類這樣比較清晰和明確。<sup>[[link](#redundant-exception)]</sup>

    ```ruby
    # 錯誤
    raise RuntimeError, 'message'

    # 正確一點 - RuntimeError 是默認的
    raise 'message'

    # 最好
    class MyExplicitError < RuntimeError; end
    raise MyExplicitError
    ```

* <a name="rescue-as-modifier"></a>避免使用 rescue 的變異形式。
    <sup>[[link](#rescue-as-modifier)]</sup>

    ```ruby
    # 錯誤
    read_file rescue handle_error($!)

    # 正確
    begin
      read_file
    rescue Errno:ENOENT => ex
      handle_error(ex)
    end
    ```

## 集合 (Collections)

* <a name="map-over-collect"></a>儘量用 `map` 而不是  `collect`。<sup>[[link](#map-over-collect)]</sup>

* <a name="detect-over-find"></a>儘量用 `detect` 而不是 `find`。 `find`
    容易和 ActiveRecord 的 `find` 搞混 - `detect` 則是明確的說明了
    是要操作 Ruby 的集合, 而不是 ActiveRecord 對象。
    <sup>[[link](#detect-over-find)]</sup>

* <a name="reduce-over-inject"></a>儘量用 `reduce` 而不是 `inject`。
    <sup>[[link](#reduce-over-inject)]</sup>

* <a name="size-over-count"></a>儘量用 `size`， 而不是  `length` 或者 `count`， 出於性能理由。<sup>[[link](#size-over-count)]</sup>

* <a name="empty-collection-literals"></a>儘量用數組和 hash 字面量來創建，
    而不是用 new。 除非你需要傳參數。
    <sup>[[link](#empty-collection-literals)]</sup>

    ```ruby
    # 錯誤
    arr = Array.new
    hash = Hash.new

    # 正確
    arr = []
    hash = {}

    # 正確, 因為構造函數需要參數
    x = Hash.new { |h, k| h[k] = {} }
    ```

* <a name="array-join"></a>為了可讀性傾向於用 `Array#join` 而不是 `Array#*`。
    <sup>[[link](#array-join)]</sup>

    ```ruby
    # 錯誤
    %w(one two three) * ', '
    # => 'one, two, three'

    # 正確
    %w(one two three).join(', ')
    # => 'one, two, three'
    ```

* <a name="symbol-keys"></a>用 符號(symbols) 而不是 字符串(strings) 作為 hash keys。
    <sup>[[link](#symbol-keys)]</sup>

    ```ruby
    # 錯誤
    hash = { 'one' => 1, 'two' => 2, 'three' => 3 }

    # 正確
    hash = { :one => 1, :two => 2, :three => 3 }
    ```

* <a name="symbol-literals"></a>如果可以的話, 用普通的 symbol 而不是字符串 symbol。<sup>[[link](#symbol-literals)]</sup>

    ```ruby
    # 錯誤
    :"symbol"

    # 正確
    :symbol
    ```

* <a name="deprecated-hash-methods"></a>用 `Hash#key?` 而不是 `Hash#has_key?`
    用 `Hash#value?` 而不是 `Hash#has_value?`.
    根據 Matz 的說法, 長一點的那種寫法在考慮要廢棄掉。
    <sup>[[link](#deprecated-hash-methods")</sup>

    ```ruby
    # 錯誤
    hash.has_key?(:test)
    hash.has_value?(value)

    # 正確
    hash.key?(:test)
    hash.value?(value)
    ```

* <a name="multiline-hashes"></a>用多行 hashes 使得代碼更可讀, 逗號放末尾。
    <sup>[[link](#multiline-hashes)]</sup>

    ```ruby
    hash = {
      :protocol => 'https',
      :only_path => false,
      :controller => :users,
      :action => :set_password,
      :redirect => @redirect_url,
      :secret => @secret,
    }
    ```

* <a name="array-trailing-comma"></a>如果是多行數組，用逗號結尾。<sup>[[link](#array-trailing-comma)]</sup>

    ```ruby
    # 正確
    array = [1, 2, 3]

    # 正確
    array = [
      "car",
      "bear",
      "plane",
      "zoo",
    ]
    ```

## 字符串 (Strings)

* <a name="string-interpolation"></a>儘量使用字符串插值，而不是字符串拼接<sup>[[link](#string-interpolation)]</sup>

    ```ruby
    # 錯誤
    email_with_name = user.name + ' <' + user.email + '>'

    # 正確
    email_with_name = "#{user.name} <#{user.email}>"
    ```

   另外，記住 Ruby 1.9 風格的字符串插值。比如說你要構造出緩存的 key 名：

    ```ruby
    CACHE_KEY = '_store'

    cache.write(@user.id + CACHE_KEY)
    ```

    那麼建議用字符串插值而不是字符串拼接:

    ```ruby
    CACHE_KEY = '%d_store'

    cache.write(CACHE_KEY % @user.id)
    ```

* <a name="string-concatenation"></a>在需要構建大數據塊時，避免使用 `String#+`。
    而是用 `String#<<`. 它可以原位拼接字符串而且它總是快於 `String#+`,
    這種用加號的語法會創建一堆新的字符串對象.<sup>[[link](#string-concatenation)]</sup>

    ```ruby
    # 正確而且快
    html = ''
    html << '<h1>Page title</h1>'

    paragraphs.each do |paragraph|
      html << "<p>#{paragraph}</p>"
    end
    ```

* <a name="multi-line-strings"></a>對於多行字符串， 在行末使用 `\` ，而不是 `+`
    或者 `<<`
    <sup>[[link](#multi-line-strings)]</sup>

    ```ruby
    # 錯誤
    "Some string is really long and " +
      "spans multiple lines."

    "Some string is really long and " <<
      "spans multiple lines."

    # 正確
    "Some string is really long and " \
      "spans multiple lines."
    ```

## 正則表達式 (Regular Expressions)

* <a name="regex-named-groups"></a>避免使用 `$1-9` 因為可能難以辨認出是哪一個，取個名。
    <sup>[[link](#regex-named-groups)]</sup>

    ```ruby
    # 錯誤
    /(regexp)/ =~ string
    ...
    process $1

    # 正確
    /(?<meaningful_var>regexp)/ =~ string
    ...
    process meaningful_var
    ```

* <a name="caret-and-dollar-regexp"></a>小心使用 `^` 和 `$` 因為它們匹配的是
    行頭/行末，而不是某個字符串的結尾.  如果你想匹配整個字符串, 用: `\A` 和 `\z`.<sup>[[link](#caret-and-dollar-regexp)]</sup>

    ```ruby
    string = "some injection\nusername"
    string[/^username$/]   # matches
    string[/\Ausername\z/] # don't match
    ```

* <a name="comment-regexes"></a>使用 `x` 修飾符在複雜的正則表達式上。
    這使得它更可讀, 並且你可以加有用的註釋。只是要注意空格會被忽略。<sup>[[link](#comment-regexes)]</sup>

    ```ruby
    regexp = %r{
      start         # some text
      \s            # white space char
      (group)       # first group
      (?:alt1|alt2) # some alternation
      end
    }x
    ```

## 百分比字面量 (Percent Literals)

* <a name="percent-literal-delimiters"></a>統一用圓括號，不要用其他括號，
   因為它的行為更接近於一個函數調用。<sup>[[link](#percent-literal-delimiters)]</sup>

    ```ruby
    # 錯誤
    %w[date locale]
    %w{date locale}
    %w|date locale|

    # 正確
    %w(date locale)
    ```

* <a name="percent-w"></a>隨意用 `%w` <sup>[[link](#percent-w)]</sup>

    ```ruby
    STATES = %w(draft open closed)
    ```

* <a name="percent-parens"></a>在一個單行字符串裡需要 插值(interpolation) 和內嵌雙引號時使用 `%()`。
    對於多行字符串，建議用 heredocs 語法。<sup>[[link](#percent-parens)]</sup>

    ```ruby
    # 錯誤 - 不需要字符串插值
    %(<div class="text">Some text</div>)
    # 直接 '<div class="text">Some text</div>' 就行了

    # 錯誤 - 無雙引號
    %(This is #{quality} style)
    # 直接 "This is #{quality} style" 就行了

    # 錯誤 - 多行了
    %(<div>\n<span class="big">#{exclamation}</span>\n</div>)
    # 應該用 heredoc.

    # 正確 - 需要字符串插值, 有雙引號, 單行.
    %(<tr><td class="name">#{name}</td>)
    ```

* <a name="percent-r"></a>僅在需要匹配 *多於一個* '/'符號的時候使用 `%r`。<sup>[[link](#percent-r)]</sup>

    ```ruby
    # 錯誤
    %r(\s+)

    # 依然不好
    %r(^/(.*)$)
    # should be /^\/(.*)$/

    # 正確
    %r(^/blog/2011/(.*)$)
    ```

* <a name="percent-x"></a>避免使用 %x ，除非你要調用一個帶引號的命令(非常少見的情況)。
    <sup>[[link](#percent-x)]</sup>

    ```ruby
    # 錯誤
    date = %x(date)

    # 正確
    date = `date`
    echo = %x(echo `date`)
    ```

## Rails

* <a name="next-line-return"></a>當調用 `render` 或 `redirect_to` 後需要馬上"返回"時，把 `return` 放到下一行, 不要放到同一行。
    <sup>[[link](#next-line-return)]</sup>

    ```ruby
    # 錯誤
    render :text => 'Howdy' and return

    # 正確
    render :text => 'Howdy'
    return

    # still bad
    render :text => 'Howdy' and return if foo.present?

    # 正確
    if foo.present?
      render :text => 'Howdy'
      return
    end
    ```

### 範圍 (Scopes)
* <a name="scope-lambda"></a>當定義 ActiveRecord 的模型 scopes 時， 把內容用大括號包起來。
    如果不包的話, 在載入這個 class 時就會被強迫連接數據庫。
    <sup>[[link](#scope-lambda)]</sup>

    ```ruby
    # 錯誤
    scope :foo, where(:bar => 1)

    # 正確
    scope :foo, -> { where(:bar => 1) }
    ```

## 保持一致 (Be Consistent)

> 在你編輯某塊代碼時，看看周圍的代碼是什麼風格。
> 如果它們在數學操作符兩邊都放了空格，那麼你也應該這樣做。
> 如果它們的代碼註釋用 # 井號包成了一個盒子, 那麼你也應該這樣做。

> 風格指南存在的意義是 讓看代碼時能關注 "代碼說的是什麼"。
> 而不是 "代碼是怎麼說這件事的"。這份整體風格指南就是幫助你做這件事的。
> 注意局部的風格同樣重要。如果一個部分的代碼和周圍的代碼很不一樣。
> 別人讀的時候思路可能會被打斷。儘量避免這一點。

&mdash;[Google C++ Style Guide][google-c++]

[airbnb-javascript]: https://github.com/airbnb/javascript
[bbatsov-ruby]: https://github.com/bbatsov/ruby-style-guide
[github-ruby]: https://github.com/styleguide/ruby
[google-c++]: http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml
[google-c++-comments]: http://google-styleguide.googlecode.com/svn/trunk/cppguide.xml#Comments
[google-python-comments]: http://google-styleguide.googlecode.com/svn/trunk/pyguide.html#Comments
[ruby-naming-bang]: http://dablog.rubypal.com/2007/8/15/bang-methods-or-danger-will-rubyist
