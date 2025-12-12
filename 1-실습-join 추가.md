1. 회원가입 jsp 작성, 네임 조정
2. 서비스 인터페이스에 void register(MemberDTO dto); 1줄추가
3. 서비스임플.자바에 public boolean register(MemberDTO param) 부분 추가
4. 콘트롤러에 @GetMapping("/join") 부분, @PostMapping("/join") 부분 추가
5. 매퍼.자바에 MemberVO findById(String id); 1줄, void insertMember(MemberVO vo); 1줄 추가(메소드용)
6. 매퍼.엑셈엘에 mybatis용 sql쿼리 추가
