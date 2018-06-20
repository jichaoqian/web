## 这只是一个WKWebView的简单使用
* 需要注意的地方

*如果这里是加载https 时候需要注意权限认证*
`- (void)webView:(WKWebView *)webView didReceiveAuthenticationChallenge:(NSURLAuthenticationChallenge *)challenge completionHandler:(void (^)(NSURLSessionAuthChallengeDisposition, NSURLCredential * _Nullable))completionHandler {
NSLog(@"收到");
// 加载https 权限认证代理方法
if ([challenge.protectionSpace.authenticationMethod isEqualToString:NSURLAuthenticationMethodServerTrust]) {
if ([challenge previousFailureCount] == 0) {
NSURLCredential *credential = [NSURLCredential credentialForTrust:challenge.protectionSpace.serverTrust];
completionHandler(NSURLSessionAuthChallengeUseCredential, credential);
} else {
completionHandler(NSURLSessionAuthChallengeCancelAuthenticationChallenge, nil);
}
} else {
completionHandler(NSURLSessionAuthChallengeCancelAuthenticationChallenge, nil);
}
}`
