# 테이블  

### 하이픈 : - 
  - 각 열의 헤더를 만드는 데 사용 (헤더 행의 각 열에 최소 3개 있어야함) 
  - 왼쪽 또는 오른쪽 또는 양쪽에 ' : ' 을 포함 시켜 왼쪽 , 오른쪽, 중앙에 텍스트를 정렬할 수 있음  

### 파이프 : |  
  - 각 열을 분리

*ex)*  

**[입력]**  
\| foo | bar |  
\| --- | --- |  
\| baz | bim |  

**[출력]**  
| foo | bar |
| --- | --- |
| baz | bim |

---

  ### 한 열의 셀 길이가 일치할 필요`X` ( 셀의 길이가 일치하면 더 쉽게 읽을 수 있음)  
  ### 선행 및 후행 파이프의 사용 일관되지 않아도 됨  

  *ex)*  
  
  **[입력]**   
  \| abc | defghi |  
  \:-: | -----------:  
  bar | baz  
  
  **[출력]**  
  | abc | defghi |
  :-: | -----------:
  bar | baz
  
  ---
  
  ### 셀에 파이프를 포함시키는 경우 
  - `\` 사용   
  
  *ex)*  
  
  **[입력]**    
  \| f\|oo  |  
  \| ------ |  
  \| b `\|` az |  
  \| b **\|** im |  
  
  **[출력]**  
  | f\|oo  |
  | ------ |
  | b `\|` az |
  | b **\|** im |  
  
  ---
  
  ### 테이블 끊기  
  - 다른 블록 구조의 시작( `ex) 블록 따옴표 ' > '` ) 시 테이블 끊어짐  
 
  *ex)*  
  
  **[입력]**  
  \| abc | def |  
  \| --- | --- |  
  \| bar | baz |  
  \> bar
  
  **[출력]**  
  | abc | def |
  | --- | --- |
  | bar | baz |
  > bar
  
  - `빈 줄` 입력시 테이블 끊어짐 
  
  *ex)* 
  
  **[입력]**  
  \| abc | def |  
  \| --- | --- |  
  \| bar | baz |  
  bar  

  bar  
  
  **[출력]**  
  | abc | def |
  | --- | --- |
  | bar | baz |
  bar

  bar
  
  ---
  
  ### 헤더 행(하이픈 행) 셀 수는 구분자 셀 수와 일치해야함 ( 그렇지 않은 경우 테이블 인식X )
  
  *ex)* 테이블로 인식되지 않음 ( 헤더 행 셀 1개 != 구분자 셀 2개 )
  
  | abc | def |  
  | --- |  
  | bar |  

  ---

  ### 헤더 행(하이픈 행) 아래 행들의 셀 수는 헤더 행 셀 수와 다를 수 있음  
  - 헤더 행 셀 수 `>`  헤더 아래 행 셀 수  
  > 빈 셀 삽입  
  - 헤더 행 셀 수 `<`  헤더 아래 행 셀 수  
  > 초과된 셀 무시(삭제됨)  
  
  *ex)*
  
  **[입력]**  
  \| abc | def |  
  \| --- | --- |  
  \| bar |  
  \| bar | baz | boo |  
  
  **[출력]**  
  | abc | def |
  | --- | --- |
  | bar |
  | bar | baz | boo |
  
  ---
  
  ### 본문에 행이 없는 경우 출력 X
  
   *ex)*
   
   **[입력]**  
  \| abc | def |   
  \| --- | --- |  
  
  **[출력]**
  | abc | def |
  | --- | --- |

  ---
  
  # 업무 목록 항목
  - `'-' '공백' '[' '공백 또는 소문자/대문자 X' ']'`로 구성  
  - **대괄호 사이 문자가 공백인 경우** : 선택 취소
  - **그렇지 않은 경우** : 선택
  
  *ex)*   
  
  **[입력]**  
  \- [ ] foo  
  \- [x] bar  

  **[출력]**  
  - [ ] foo  
  - [x] bar 

  ---

  ### 들여쓰기로 중첩 가능
  
  *ex)*  
  
  **[입력]**  
  \- [x] foo  
  \  - [ ] bar  
  \  - [x] baz  
  \- [ ] bim  
  
  **[출력]**  
  - [x] foo  
    - [ ] bar  
    - [x] baz  
  - [ ] bim

  ---
  
  # 취소선
  - ' ~~ ' 로 사용가능  
 
  *ex)*  
  
  **[입력]** \~~안녕하세요~~ 저는 숭실대학교 학생입니다.
  
  **[출력]**
  ~~안녕하세요~~ 저는 숭실대학교 학생입니다.
  
  - 빈 줄 입력 시 취소선 중단됨    
  
  *ex)*  
  
  오늘은 ~~미세먼지가
  
  너무 심해요~~
  
  ---
  
  # 자동 링크
  
  ## 텍스트 발견 후 유효한 도메인이 있을 때 확장된 www 자동 링크 인식
  
  ### http 자동 삽입  
  - www.commonmark.org
  
  ### 유효한 도메인 이후에 공백이 없는 문자가 붙을 수 있음  
  - Visit www.commonmark.org/helpfor more information.

  ## 확장 자동 링크 경로 유효성 검사를 다음과 같이 적용
  
  ### 후행 구두점(?, !, ., , , :, *, _, ~)은 링크 내부에 포함될 수 있지만 자동 링크의 일부로 간주되지 않음.
  
  - Visit www.commonmark.org.

  - Visit www.commonmark.org/a.b. -> 유효하지 않는 링크
   
   ### 괄호 수 검사
   - 여는 괄호보다 닫히는 괄호 수가 더 많은 경우, 자동 링크의 일치하지 않는 후행 괄호 고려X
   
     www.google.com/search?q=Markup+(business)

     www.google.com/search?q=Markup+(business)))

     (www.google.com/search?q=Markup+(business))

     (www.google.com/search?q=Markup+(business)
     
   - -> 4개의 링크 모두 구글 창에 Markup (business) 검색
    
   ### 검사는 링크가 닫는 괄호로 끝날 때만 수행되므로, 자동 링크 내부에 괄호만 있는 경우 다음과 같은 특별한 규칙 적용X
   - www.google.com/search?q=(business))+ok
   - -> 구글 창에 (business)) ok 검색
    
   ### 자동 링크가 ; 로 끝나는 경우 & 뒤에 텍스트 자동링크에서 제외
   
   - www.google.com/search?q=commonmark&hl=en

   - www.google.com/search?q=commonmark&hl;

   - -> 2개 링크 모두 구글 창에 commonmark 검색
    
   ### 링크 사이에 `<` 입력시 자동 링크 종료
   
   - www.commonmark.org/he<lp
    
   ### 확장 URL 자동 링크는 http:// 또는 https:// 뒤에 유효한 도메인이 있는 다음 공백이 아닌 문자를 사용할 때 인식됨
   
   - http://commonmark.org

   - (Visit https://encrypted.google.com/search?q=Markup+(business))
    
   ### 이메일 링크
   - 텍스트 내에 이메일 주소가 인식되면 확장된 이메일 자동 링크가 인식
   - 이메일 주소는 다음 규칙을 따라야 함
      - 영숫자 또는 ., -, _, +인 하나 이상의 문자
      - @ 기호
      - 마지막 문자는 - 또는 _ 중 하나일 수 없음
   - 메일 수신자가 생성된 링크에 자동으로 추가됨
   
   - youro1228@naver.com
   
   ### 이메일 내 `+` 사용
   - @ **앞** 텍스트에서는 + 사용 **가능**
   - @ **뒤** 텍스트에서는 + 사용 **불가능**
   
   - youro1228@na+ver.com
   - youro+1228@naver.com

   ### 이메일 내 ` . - _ ` 사용
   - . - _ 는 @의 양쪽에서 사용가능
   - . 만 메일 주소 끝에서 사용 가능 ( 이 경우에는 주소의 일부로 간주되지 않음 )
   
   - > a.b-c_d@a.b

   - > a.b-c_d@a.b.

   - > a.b-c_d@a.b-

   - > a.b-c_d@a.b_
    
  ## 허용되지 않는 원시 HTML
  - 선행 < 을 \&lt; 로 대체하여 수행
  - 이러한 태그들은 HTML이 그들 고유의 방식으로 해석되는 방법을 변경할 때 선택됨 ( 중첩된 HTML은 다르게 해석 )
  - 다른 모든 HTML 태그는 그대로 유지
    - <title>
    - <textarea>
    - <style>
    - <xmp>
    - <iframe>
    - <noembed>
    - <noframes>
    - <script>
    - <plaintext>

  *ex)*  
  **[입력]**   
  \<strong> <title> <style> \<em>  
  \
  \<blockquote>  
  \ <xmp> is disallowed.  <XMP> is also disallowed.  
  \</blockquote>  
     
  **[출력]**    
  <strong> <title> <style> <em>

  <blockquote>
   <xmp> is disallowed.  <XMP> is also disallowed.
  </blockquote>
