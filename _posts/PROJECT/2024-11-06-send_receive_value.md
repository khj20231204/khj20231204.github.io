---
layout: single
title: 서버와 클라이언트가 값 넘겨주고 받기
categories: PROJECT
tag: []
author_profile: false
---   

1. # 값 넘겨주고 받기

1. # map 이용
   map : server   
   ```java
      public ResponseEntity<Map<String, Object>> noticelist(
               @RequestParam(value="page", defaultValue = "1") int page,
               @RequestParam(value="size" ,defaultValue = "10") int size){
            
         int start = (page - 1) * size;
         
         Map m = new HashMap<>();
         m.put("start", start);
         m.put("size", size);
         
         List<NoticeDto> noticeList = noticeService.getNoticeList(m);
         System.out.println("페이지 : "+ page +" 글목록 :" + noticeList);
         
         Map<String, Object> map = new HashMap<>();
         
         map.put("notices", noticeList);
         map.put("page", page);
         map.put("size", size);
         
         return new ResponseEntity<>(map, HttpStatus.OK);
      }
   ```

   Map으로 받기 : client   
   ```javascript
      const [notices, setNotices] = useState([]); //배열로 선언

      const response = await axios.get(`/api/notice/noticelist?page=${page}`);
      const nextData = response.data.notices;
      setNotices((prevData) => [...prevData, ...nextData]);
      setPage((page) => page + 1);
   ```

   map사용
   ```javascript

      {notices.map((noticeData) => (
         return (   //return 사용
            <NoticeListItem
               key={noticeData.postNo}
               noticeData={noticeData}
               onClick={() => onClickItem(noticeData)}
            />
         )
      ))}
      {loading && <div>Loading...</div>}
   ```

1. # 주소 mapping값 받기
   PathVariable : server
   ```java

      @GetMapping("/communitycontent/{postNo}")  //postNo 받기
      public ResponseEntity<CommunityDto>communitycontent(@PathVariable("postNo") int postNo)throws Exception{
         
         communityService.updateVw(postNo); 
         CommunityDto community = communityService.getCommunity(postNo);
         
         return new ResponseEntity<>(community,HttpStatus.OK); //클래스로 돌려주기
      }
   ```

   PathVariable : client   
   ```javascript
      useEffect(()=>{
        axios.get(`/api/community/communitycontent/${postNo}`)
        .then(response=>{
            setSelectedCommunity(response.data);
            setTitle(response.data.title);
            setContent(response.data.content);
        })
   ```

1. # 주소 변수 값 받기(int형이든 String형이든 받을 때 결정해 주면 됨)

   RequestParam : server   
   ```java
      @GetMapping("/api/getRoomInfo") 
      public ResponseEntity<Map<String, Object>> getRoomInfo(@RequestParam("roomNo") int roomNo) { //여기서 roomNo의 데이터형 결정
         Map<String, Object> responseBody =new HashMap<String, Object>();
         try {
            MafiaRoom getRoomInfo = mafiaService.getRoomInfo(roomNo);
            responseBody.put("msg", "[방 대기] 방 정보 조회 성공!");
            responseBody.put("방 대기 정보", getRoomInfo);
            
            // 200
            return ResponseEntity.status(HttpStatus.OK).body(responseBody);
         } catch (Exception e) {
            responseBody.put("msg", "[방 대기] 방 정보 조회 실패ㅠ");
            
            // 500
            return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body(responseBody);
         }
      }
   ```
   roomNo를 문자열로 받고 싶으면 `(@RequestParam("roomNo") String roomNo)` 으로 작성하면 됨   

   RequestParam : client
   ```javascript   

      const [gameInfo, setGameInfo] = useState([]);
      const [gameParty, setGameParty] = useState([]);
      const [pageState, setPageState] = useState(0);

      useEffect(() => {
         const fetchGameInfo = async () => {
            
            const response = await axios.get(`/api/getRoomInfo?roomNo=${roomNo}`);
            setGameInfo(response.data["방 대기 정보"]);
            setPageState(response.data["방 대기 정보"].isOnGame);
            console.log(pageState);
            if (response.data["방 대기 정보"].isOnGame === 1) {
               navigate(`/onGame/${roomNo}`);
               window.location.reload();
            }
         
         // 5초 후에 다시 실행하도록 설정
         setTimeout(fetchGameInfo, 5000); // 5초(5000밀리초) 후에 다시 호출
      };
   ```

1. # 객체 넘기기

   RequestBody : server   
   ```java

      @PostMapping("/api/addmember")
	   public ResponseEntity<String> addMember(@RequestBody MemberDto memberDto) {
	      boolean success = memberService.addMember(memberDto);
	      if (success) {
	         return ResponseEntity.ok("회원가입이 성공적으로 처리되었습니다.");
	      } else {
	         return ResponseEntity.badRequest().body("회원가입실패, ID ,닉네임, 이메일 , 휴대폰번호 중복검사 해주세요");
	      }
	   }

      - MmeberDto 클래스-
      public class MemberDto {
	
         private String userId;
         private String passWd;
         private String userName;
         private String nickName;
         private String profileImagePath;
         private String phoneNum1;
         private String phoneNum2;
         private String phoneNum3;	
         private String emailNum1;
         private String emailNum2;
         private String birth;
         private String gender;
         
         private String userAuthority = "user";
         private int withdrawal = 1; 
      }
   ```

   ReqeustBody : client   
   ```javascript

      const handleSubmit = async () => {
         const userInfo = {
            userId,
            nickName,
            userName: username,
            passWd: password,
            profileImagePath: profileImage ? profileImage.name : '',
            phoneNum1,
            phoneNum2,
            phoneNum3,
            emailNum1,
            emailNum2: emailDomain,
            birth,
            gender: gender === "male" ? "M" : "F",
         };
            try {
               const response1 = await axios.post('/api/addmember', userInfo, {
               headers: {
                  'Content-Type': 'application/json'
               }
            });
         }
      }
   ```

1. # 이미지 파일 받기

   RequestPart : server
   ```java
      @PostMapping("/api/addmember/image")
      public String addMemberImage(@RequestPart("profileImage") MultipartFile profileImage)
      {
         if (profileImage != null && !profileImage.isEmpty()) {
            String imagePath = memberService.saveImage(profileImage);
            if (imagePath != null) {
                  return "프로필 이미지가 성공적으로 업로드되었습니다.";
            } else {
                  return "이미지 파일 저장에 실패했습니다.";
            }
         } else {
            return "이미지 파일이 비어있습니다. 회원가입완료";
         }
      }
   ```

   ```javascript
      if (profileImage) {
         const formData = new FormData();
         formData.append('profileImage', profileImage);

         const response2 = await axios.post('/api/addmember/image', formData);

         if (response1.status === 200 && response2.status === 200) {
            const data1 = response1.data;
            const data2 = response2.data;
         } else {
            alert('회원가입(중복검사 해주세요) 또는 이미지 업로드에 실패했습니다.');
         }
      }
   ```

1. # 변수 2개 전송

   -server-   
   ```java
      @GetMapping("/noticelist")
      public ResponseEntity<Map<String, Object>> noticelist(
            @RequestParam(value="page", defaultValue = "1") int page,
            @RequestParam(value="size" ,defaultValue = "10") int size){
         
         int start = (page - 1) * size;
         
         Map m = new HashMap<>();
         m.put("start", start);
         m.put("size", size);
         
         List<NoticeDto> noticeList = noticeService.getNoticeList(m);
         System.out.println("페이지 : "+ page +" 글목록 :" + noticeList);
         
         Map<String, Object> map = new HashMap<>();
         
         map.put("notices", noticeList);
         map.put("page", page);
         map.put("size", size);
         
         return new ResponseEntity<>(map, HttpStatus.OK);
      }
   ```

   -client-   
   ```javascript
      const fetchData = async () => {
         setLoading(true);
         try {
               const response = await axios.get(`/api/notice/noticelist?page=${page}`);
               const nextData = response.data.notices;
               setNotices((prevData) => [...prevData, ...nextData]);
               setPage((page) => page + 1);
               setHasMore(nextData.length > 0);
         } catch (error) {
               console.error("Error fetching data:", error);
         } finally {
               setLoading(false);
         }
      };
   ```