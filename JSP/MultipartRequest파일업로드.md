# MultipartRequest를 이용해서 파일 업로드하기

시작전 [`cos.jar`](http://www.servlets.com)를 먼저 다운 받아서
WEB-INF/lib 폴더 안에 붙여 넣자

<br>

### View
> form의 enctype을 multipart/form-data로 설정해야 합니다.
```html
<form action="경로" method="post" enctype="multipart/form-data">
    이름 : <input type="text" name="userName">
    사진 : <input type="file" name="upfile">

    <button type="submit">전송</button>
</form>
```

<br>

### Controller
```java
// 인코딩 설정을 할 때 POST방식은 값을 받는 서블릿에서 설정해주여야 합니다.
request.setCharacterEncoding("UTF-8");

// session을 전역으로 사용할 수 있도록 조건식 밖에 선언해줍니다.
HttpSession session = request.getSession();

// multipart/form-data방식으로 요청을 성공했을 때만 구문을 실행하도록 조건식을 만들어줍니다.
if(ServletFileUpload.isMultipartContent(request)){

    // getRealPath를 이용해서 파일이 저장될 서버의 경로를 얻어올 수 있습니다.
    String savaPath = session.getServletContext().getRealPath("저장할 폴더 경로/");

    // 업로드할 수 있는 최대 파일 크기를 제한해둡니다.
    // 저는 20mbyte로 지정하고자 했습니다.
    // 공식을 풀어보자면 1024 * 1024는 1mbyte입니다. 여기서 20을 곱해 20mbyte를 만들었습니다.
    int maxSize = 1024 * 1024 * 20

    // savePath와 maxSize를 구하는 이유는 MultipartRequest를 생성하기 위해 매개변수로 필요하기 때문입니다.
    // MultipartRequest를 생성하면 submit했을 때 지정된 경로에 파일 업로드가 가능해집니다.
    //                                 request객체─┐      파일최대크기─┐         파일명중복방지처리─┐
    MultipartRequest multi = new MultipartRequest(request, savePath, maxSize, "UTF-8", new MyFileRenamePolicy())
    //                                                      └─저장서버경로       └─인코딩방식



    //─── DB에 데이터 저장 ───

    // multipart/form-data로 submit한 데이터들은 request객체가 아니라 MultipartRequest객체로 가져와야합니다.
    // 그래서 request.getParameter가 아닌 multi.getParameter를 사용해야 합니다.(여기서 multi는 위에서 선언한 변수명 입니다.)
    String userName = multi.getParameter("userName");

    // Attachment객체를 전역으로 빼내서 매개변수로 사용하기 위함과 넘어온 첨부파일이 있을때 생성하기 위해 미리 선언만 해둡니다.
    Attachment attachment = null;

    // multiRequest.getOriginFileName("키값")은 넘어온 첨부파일의 파일명을 가져옵니다.
    // 넘어온 첨부파일이 없어서 파일명이 없다면 null입니다.
    if(multiRequest.getOriginFileName("upfile") != null){

        // 넘어온 첨부파일이 있어서 attachment객체를 매개변수 생성자로 생성 합니다.
        attachment = new Attachment();

        // DB에 insert할때 필요한 값을 넣어줍니다.(원본명, 수정된파일명, 저장경로 등등)
        attachment.setOriginName(multiRequest.getOriginFileName("upfile")); // => 넘어온 파일의 파일명(원본)
        attachment.setChangeName(multiRequest.getFilesystemName("upfile")); // => 서버에 실제로 업로드된 파일명(수정본)
        attachment.setFilePath("파일보관경로/");

        // 이후에 Service객체가 있다면 데이터를 받았던 userName, attachment를 매개변수로 보내 처리를 하면 됩니다.
    }
}
```