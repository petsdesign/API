# 주문접수 API

## Request (POST) ##
<p>주문 요청 URL: http://api.petsdesign.co.kr/order</p>
<p>테스트 주문 요청URL: http://api.petsdesign.co.kr/order/test</p>
<p>Require header: pd_key (해당키는 펫츠디자인 개발팀에 발급요청 하시기바랍니다. dev@petsdesign.co.kr)</p>

## Response parameters ##

<ul>
	<li>data: 주문정보 (JSON 형식)</li>
</ul>

``` js
{
	"oaType": null, //[default: "api", string]
	//제휴처: storefarm(스토어팜), emp(EMP), talkstore(톡스토어), mall(자사몰)
	//제휴처별 주문관리를 위한 항목입니다. 제휴처 주문값이 없을경우 해당 파라미터 값을 null 또는 "api" 로 요청 합니다.
	
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
	
	"bankSender": "펫투비", //[Conditional Required, string]
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

## Response (JSON) ##

### 주문접수 성공시 ###

``` js
{
    "payResult": { //결제결과
        "successs": 0, //성공여부 (1 => 성공, 0 => 실패)
        "payResultMsg": "order test :)", //결제결과 메세지
        "cashBalance": "0", //현재 캐쉬 잔액 (결제성공시에는 결제후 잔액)
        "payAmount": "7600" //결제요청 금액
    },
    "orderResult": { //주문접수 결과
        "success": "1", //성공여부 (1 => 성공, 0 => 실패)
        "ordNo": "1525145229154", //주문번호
        "oaType": "api", //제휴처 (api => oAPI를 이용한 일반 펫투비 주문을 뜻함)
        "oaApiOrdno": "123456", //제휴처 주문번호
        "nameReceiver": "펫츠디자인", //받는사람
        "zipCode": "", //우편번호
        "address": "경기도 화성시 팔탄면 버들로 1362번길 10-12 펫츠디자인", //주소
        "orderGoods": "[테스트] 일반상품 외 2건", //주문상품내용 요약
        "settleKind": "a", //결제방법
        "settlePrice": "7600", //총 결제금액
        "totalGoodsPrice": "5100", //총 상품금액
        "delivery": "2500" //배송비,
        "memo": "부재시 경비실에 맡겨주세요!" //배송 메세지 (주문 테스트인경우 요청 파라미터가 삽입되어 리턴 됩니다.)
    }
}
```


## Code sample ##
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
