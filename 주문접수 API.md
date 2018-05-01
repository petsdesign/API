# 주문접수 API

### Request (POST) ###
<p>주문 요청 URL: http://api.petsdesign.co.kr/order</p>
<p>테스트 주문 요청URL: http://api.petsdesign.co.kr/order/test</p>
<p>Require header: pd_key (해당키는 펫츠디자인 개발팀에 발급요청 하시기바랍니다. dev@petsdesign.co.kr)</p>

### Response parameters ###

<ul>
	<li>data: 주문정보 (JSON 형식)</li>
</ul>

``` js
{
	"oaType": "pettob" //[default: "pettob, string]
	//제휴처: pettob(일반), storefarm(스토어팜), emp(EMP), talkstore(톡스토어), mall(자사몰)
	
	"oaOrderNo": "123456", //[default: null, string]
	//제휴처 주문번호: null 인경우 자동으로 생성되며, 중복주문 확인 또는 주문조회시 사용 됩니다.
	
	"nameReceiver": "펫츠디자인", //[Required, string]
	//수령자: 2글자 이상의 수령자 이름
	
	"phoneReceiver": "010-1234-5678", //[Required, string]
	//수령자 전화번호1
	
	"mobileReceiver": "010-1234-5678", //[Required, string]
	//수령자 전화번호2
	
	"zipCode": "12345", //[Required, string]
	//(구/신)우편번호: 5자리 이상의 구 우편번호 또는 신 우편번호
	
	"address": "경기도 화성시 팔탄면 버들로 1362번길 10-12", //[Required, string]
	//(지번/도로명)주소: 주소정재 API를 이용하기 때문에 가급적 신주소로 요청하시기 바랍니다.
	
	"address2": "펫츠디자인", //[Required, string]
	//나머지 주소: 아파트명, 동, 호수 등 나머지 주소
	
	"settleKind": "a", //[default: "a", string]
	//결제방식: "a" => (무통장), "s" => (캐쉬결제)
	//무통장 결제인 경우, 주문접수만 처리 하고 캐쉬결제인 경우 주문접수후 캐쉬결제까지 처리합니다.
	
	"bankSender": "펫투비",  //[Conditional Required, string]
	//입금자명: settleKind 파라미터가 "a" (무통장)인경우 필수
	
	"doubleCheck": "1", //[Required, int]
	//구매동의: 구매하는 상품의 결제정보를 확인 하였으며, 구매진행의 동의여부 (1 => 동의, 0 => 동의하지 않음)
	//*동의하지 않을경우 주문접수 불가 합니다.
	
	"memo": "부재시 경비실에 맡겨주세요!", //[default: null, string]
	//배송메세지: 최대 100글자
	
	"orderItem": [ //[Required, array]
	// 주문상품 정보
		{
			"goodsNo": 7373, //[Required, int]
			//주문 상품번호: 펫투비 상품번호
			
			"ea": 1 //[Required, int]
			//주문수량: 1 이상의 양수
		},
		{
			"goodsNo": 10437,
			"ea": 2
		},
		{
			"goodsNo": 10438,
			"ea": 3
		}
	]
}
```

### Response (JSON) ###
<ul>
  <li>orderNo: 주문번호</li>
  <li>oaType: OA타입</li>
  <li>oaOrderNo: OA주문번호</li>
  <li>orderName: 주문자명</li>
  <li>orderPhone: 주문자 전화번호</li>
  <li>orderCellPhone: 주문자 휴대폰번호</li>
  <li>receiverName: 수취인명</li>
  <li>receiverPhone: 수취인 전화번호</li>
  <li>receiverCellPhone: 수취인 휴대폰번호</li>
  <li>receiverZonecode: 수취인 우편번호(신)</li>
  <li>receiverRoadAddress: 수취인 도로명주소(전체)</li>
  <li>receiverZipcode: 수취인 우편번호(구)</li>
  <li>receiverAddress: 수취인 주소(전체)</li>
  <li>orderMemo: 배송메세지</li>
  <li>settlePrice: 결제금액</li>
  <li>deliveryType: 배송타입</li>
  <li>deliveryCharge: 배송비</li>
  <li>invoiceCompanySno: 배송사코드</li>
	<ul>
		<li>12: 한진택배</li>
		<li>15: CJ대한통운</li>
		<li>21: KG로지스</li>
	</ul>
  <li>invoiceCompanyNm: 배송사명</li>
  <li>invoiceNo: 송장번호</li>
  <li>orderStatus: 주문상태</li>
	<ul>
		<li>0: 주문접수</li>
		<li>1: 결제완료</li>
		<li>2: 상품준비중</li>
		<li>3: 출고완료</li>
	</ul>
  <li>orderClaimStatus: 주문클레임상태</li>
	<ul>
		<li>0: null</li>
		<li>40: 취소요청</li>
		<li>41: 취소접수</li>
		<li>42: 취소진행</li>
		<li>44: 취소완료</li>
		<li>50: 결제시도</li>
		<li>51: PG에러</li>
		<li>54: 결제실패</li>
	</ul>
  <li>insStatus: 검수상태</li>
	<ul>
		<li>0: null</li>
		<li>1: 검수중</li>
		<li>2: Boxing</li>
		<li>3: 검수완료</li>
		<li>10: 검수불가</li>
		<li>11: 입고대기</li>
	</ul>
  <li>insEprDt: 출고가능날짜</li>
  <li>regDt: 주문접수일</li>
  <li>paymentDt: 결제완료일</li>
  <li>deliveryDt: 출고일</li>
  <li>modDt: 최근수정일</li>
  
  <li>(array)item: 주문상품</li>
	<ul>
		<li>goodsNo: 상품고유번호</li>
		<li>goodsNm: 상품명</li>
		<li>makerNm: 제조사</li>
		<li>brandNm: 브랜드</li>
		<li>goodsPrice: 판매가격</li>
		<li>orderCnt: 주문수량</li>
	</ul>
  
</ul>

### Code sample ###
<blockquote>
	<p>cURL</p>
</blockquote>
<pre>
	<code>
		curl -X GET
		http://api.petsdesign.co.kr/order/{주문번호}[/{OA타입}]
		-H 'cache-control: no-cache'
		-H 'pd_key: {발급받은 API key}'
	</code>
</pre>
