## try-finally 보다는 try-with-resources를 사용하라
- 자원을 열고 닫는 작업에서는 try-finally 대신 try-with-resources 구문을 사용해야 한다.  
자원을 자동으로 닫아주기 때문에 코드가 더 간결하고 안전해진다.
  
### try-finally를 사용 경우

```
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
    // 파일을 읽는 작업 수행
} catch (IOException e) {
    // 예외 처리
} finally {
    if (br != null) {
        try {
            br.close();
        } catch (IOException e) {
            // 닫기 예외 처리
        }
    }
}
```
### try-with-resources를 사용할 경우 
 
```
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    // 파일을 읽는 작업 수행
} catch (IOException e) {
    // 예외 처리
}
```
