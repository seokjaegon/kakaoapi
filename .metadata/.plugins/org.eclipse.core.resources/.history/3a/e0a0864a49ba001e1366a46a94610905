package kr.co.icia.mapline.controller;

import java.io.IOException;
import java.util.List;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;

import com.fasterxml.jackson.databind.ObjectMapper;

import kr.co.icia.mapline.util.KakaoApiUtil;
import kr.co.icia.mapline.util.KakaoApiUtil.Point;

@Controller
public class MapController {

	/**
	 * 자동차 이동 경로 그리기
	 * 
	 * @param fromAddress 출발지 주소정보
	 * @param toAddress   목적지 주소정보
	 * @param model       html파일에 값을 전달해주는 객체
	 * @return html 파일위치
	 * 
	 */
	@GetMapping("/map/paths") // url : /map/paths
	public String getMapPaths(@RequestParam(required = false) String fromAddress, // 출발지 주소 정보를 요청 파라미터로 받아온다
			@RequestParam(required = false) String toAddress, // 도착지 주소 정보를 요청 파라미터로 받아온다.
			Model model // 뷰에 데이터를 전달하기 위한 객체이다.
			) throws IOException, InterruptedException {
		// fromPoint(출발지), toPoint(도착지) 초기값 설정
		Point fromPoint = null;
		Point toPoint = null;
		// 만약 출발지 주소가 null이 아니고 비어있지 않으면
		if (fromAddress != null && !fromAddress.isEmpty()) {
			// fromPoint(출발지)에 출발지 주소의 위도와 경도 값을 받는다.
			fromPoint = KakaoApiUtil.getPointByAddress(fromAddress);
			// "fromPoint"라는 변수로 fromPoint(출발지)의 값을 paths.html로 전달한다.
			model.addAttribute("fromPoint", fromPoint);
		}
		// 만약 도착지 주소가 null이 아니고 비어있지 않으면
		if (toAddress != null && !toAddress.isEmpty()) {
			// toPoint(도착지)에 도착지 주소의 위도와 경도 값을 받는다.
			toPoint = KakaoApiUtil.getPointByAddress(toAddress);
			// "toPoint"라는 변수로 toPoint(도착지)의 값을 paths.html로 전달한다.
			model.addAttribute("toPoint", toPoint);
		}
		// 만약 fromPoint(출발지)와 toPoint(도착지) 둘다 null이 아니면
		if (fromPoint != null && toPoint != null) {
			// pointList에 fromPoint(출발지)에서 toPoint(도착지)까지의 차량경로를 저장한다.
			List<Point> pointList = KakaoApiUtil.getVehiclePaths(fromPoint, toPoint);
			// pointList를 JSON 형식의 문자열로 반환한다.
			String pointListJson = new ObjectMapper().writer().writeValueAsString(pointList);
			// "pointList"라는 이름으로 pointListJosn을 paths.html로 전달한다.
			model.addAttribute("pointList", pointListJson);
		}
		return "map/paths";
	}

	/**
	 * 주소를 좌표로 변환
	 * 
	 * @param address 주소정보
	 * @param model   html파일에 값을 전달해주는 객체
	 * @return html 파일위치
	 * 
	 */
	@GetMapping("/map/address/point") // url : /map/address/point
	public String getMapAddressPoint(@RequestParam(required = false) String address, Model model)
			throws IOException, InterruptedException {
		if (address != null && !address.isEmpty()) {
			Point point = KakaoApiUtil.getPointByAddress(address);
			model.addAttribute("point", point);
		}
		return "map/address_point";
	}

	/**
	 * 출발지와 목적지를 지도상에 표시하기
	 * 
	 * @param fromAddress 출발지 주소정보
	 * @param toAddress   목적지 주소정보
	 * @param model       html파일에 값을 전달해주는 객체
	 * @return html 파일위치
	 * 
	 */
	@GetMapping("/map/marker") // url : /map/marker
	public String getMapMarker(@RequestParam(required = false) String fromAddress, //
			@RequestParam(required = false) String toAddress, //
			Model model) throws IOException, InterruptedException {
		if (fromAddress != null && !fromAddress.isEmpty()) {
			Point fromPoint = KakaoApiUtil.getPointByAddress(fromAddress);
			model.addAttribute("fromPoint", fromPoint);
		}
		if (toAddress != null && !toAddress.isEmpty()) {
			Point toPoint = KakaoApiUtil.getPointByAddress(toAddress);
			model.addAttribute("toPoint", toPoint);
		}
		return "map/marker";
	}

}