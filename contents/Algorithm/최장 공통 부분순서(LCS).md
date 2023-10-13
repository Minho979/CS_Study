# 최장 공통 부분순서(LCS: Longest Common Subsequence)
- 두 문자열에 공통적으로 들어있는 공통 부분순서 중 가장 긴 문자열
- 최장 공통 문자열(Longest Common Substring) 또한 LCS라고 불림
- 최장 공통 문자열의 경우 최장 공통 부분순서를 구하는데 사용 됨

## 용어 정리
### Subsequence
- 문자열의 부분순서로 이어지지 않고 떨어져 있어도 되지만 순서는 뒤바뀌어서는 안됨
- \<bcdb\>는 문자열 \<abcbdab\>의 subsequence

### Common subsequence
- 두 문자열의 공통 부분순서
- \<bca\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 common subsequence

### Longest Common Subsequence(LCS)
- 두 문자열의 최장 공통 부분순서 (Common subsequence 중 가장 긴 것)
- \<bcba\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 LCS

### Longest Common Substring
- 두 문자열의 최장 공통 문자열로 한번에 이어져있는 문자열
- \<ab\>, \<bd\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 LCS

## 최장 공통 문자열(Longest Common Substring)



> ⬆️:[Top](#최장-공통-부분순서-LCS:-Longest-Common-Subsequence)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 그림으로 알아보는 LCS 알고리즘 - Longest Common Substring와 Longest Common Subsequence](https://velog.io/@emplam27/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-LCS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Longest-Common-Substring%EC%99%80-Longest-Common-Subsequence)
