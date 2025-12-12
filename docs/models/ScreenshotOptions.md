# Whisper.Api.Sdk.Model.ScreenshotOptions
Configuration options for screenshot capture including viewport size, format, and behavior settings.

## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**Width** | **int** | Viewport width in pixels | [optional] [default to 1920]
**Height** | **int** | Viewport height in pixels | [optional] [default to 1080]
**FullPage** | **bool** | Capture the full page height (scrolling screenshot) | [optional] [default to false]
**WaitTime** | **int** | Wait time in milliseconds before taking screenshot | [optional] [default to 2000]
**Format** | **string** | Image format for the screenshot | [optional] [default to FormatEnum.Png]
**Quality** | **int** | Image quality (1-100, only for jpeg/webp) | [optional] [default to 90]
**UserAgent** | **string** | User agent string to use for the request | [optional] 
**Javascript** | **bool** | Enable JavaScript execution | [optional] [default to true]
**BlockAds** | **bool** | Block ads and trackers | [optional] [default to false]
**AcceptCookies** | **bool** | Accept cookies consent if prompted | [optional] [default to true]

[[Back to Model list]](../../README.md#documentation-for-models) [[Back to API list]](../../README.md#documentation-for-api-endpoints) [[Back to README]](../../README.md)

