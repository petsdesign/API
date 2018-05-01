# 주문접수 API

# Request (POST)
<p>주문 요청 URL: http://api.petsdesign.co.kr/order</p>
<p>(테스트)주문 요청URL: http://api.petsdesign.co.kr/order/test</p>
<p>Require header: pd_key (해당키는 펫츠디자인 개발팀에 발급요청 하시기바랍니다. dev@petsdesign.co.kr)</p>

# Response parameters

<p>* data: 주문접수 정보 (JSON)</p>
<code>
	{
		"oaType": "pettob','storefarm', 'emp', 'talkstore', 'mall'
		"oaOrderNo": "123456",
		"nameReceiver": "홍수민",
		"phoneReceiver": "010-2280-9802",
		"mobileReceiver": "010-2280-9802",
		"zipCode": "14575",
		"address": "경기도 부천시 옥산로 16 (중동, 연화마을 건영캐스빌아파트) 1411동",
		"address2": "1402호",
		"settleKind": "a",
		"bankSender": "올라펫",
		"doubleCheck": "1",
		"memo": ".강아지때문에 경비실에 맡기신 후 연락 부탁드립니다. 감사합니다.",
		"orderItem": [
			{
				"goodsNo": 8409,
				"ea": 1
			}
		]
	}
</code>
<p>
	{OA타입} = 
	<ul>
		<li>pettob: 펫투비 주문서</li>
		<li>storefarm: 스토어팜 주문서</li>
		<li>emp: EMP(Playauto) 주문서</li>
		<li>talkstore: 톡스토어 주문서</li>
		<li>mall: 자체운영몰 주문서</li>
	</ul>
</p>

# Response (JSON)
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

# Code sample
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
