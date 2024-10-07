# 함수형 프로그래밍(Functional Programming) 연습

```java
    @Test
    void pr1() {
        List<String> list = List.of("A", "B", "C", "A", "B", "C", "D", "E", "F", "G", "H", "D", "E", "F", "D", "E", "F");
        /**
         * 영문이 key, 개수가 value인 Map을 만들라
         */

        /**                    key			value	  key 값 겹쳤을때
         * Collectors.toMap(keyMapper,valueMapper,mergeFunction)
         */
       /* Function<String, String> keyMapper = item -> item;  or */
        Function<String, String> keyMapper = Function.identity();
        Function<String, Integer> valueMapper = itemValue -> 1;
        BinaryOperator<Integer> mergeMapper = (oldValue, newValue) -> oldValue + newValue;
        Map<String, Integer> answerMap = list.stream()
                .collect(Collectors.toMap(
                        keyMapper,
                        valueMapper,
                        mergeMapper
                ));
        System.out.println("answerMap: " + answerMap);
    }
    
```
```java
    @Test
    void pr2() {
        List<Character> list = List.of('a', 'B', 'C', 'a', 'b', 'C', 'd', 'E', 'f', 'g', 'H', 'e', 'i', 'F', 'D', 'E', 'f');
        /**
         * 대문자를 제외한 소문자만 가진 List를 만들어라
         *
         * Predicate<> : 조건을 판별하는 함수형 인터페이스
         */                                             // 들어온 리스트의 아이템이 소문자냐? true or false
        Predicate<Character> lowerAlphabet = item -> Character.isLowerCase(item);
        List<Character> lowerAlphabets = list.stream()
                .filter(lowerAlphabet)
                .collect(Collectors.toList());
        System.out.println("lowerAlphabets: " + lowerAlphabets);
    }
```

