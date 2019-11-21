# ExtensionBaseImpDemo
一个便于团队或个人开发中优雅高效的统一管理类(class)扩展的方案分享(swift 版)
方案代码位于:ExtensionBaseImp.swift, 方案灵感主要来自阅读Kingfisher部分源码, 方案主要涉及到技术点:泛型, 自定义协议(protocal), 扩展(extension)

方案代码一瞥(😄):

import Foundation
import UIKit

/// 定义一个基于泛型的扩展基类
public final class ExtensionBaseImp<Base> {
    public let base: Base
    public init(_ base: Base) {
        self.base = base
    }
}


/// 定义扩展的抽象协议
public protocol ExtensionBasePro {
    associatedtype T
    var ebi: T { get }
}


/// 实现扩展的抽象协议
public extension ExtensionBasePro {
    var ebi: ExtensionBaseImp<Self> {
        get { return ExtensionBaseImp(self) }
    }
}


/// 申明需要扩展的类(class)或结构体(struct), 并是其支持ExtensionBasePro抽象协议
extension NSObject: ExtensionBasePro {}


/// 扩展限定实现: 通过标识符“:”或“==”, 为需要扩展的类(class)或结构体(struct)的扩展属性或方法
extension ExtensionBaseImp where Base: NSObject {
    
    /// 测试代码输出: Hello Swift!
    public func printLog() {
        print("Hello Swift!")
    }
    
}

extension ExtensionBaseImp where Base == UIView {
    /// 测试代码输出: Hello Swift!
    public func printLog2() {
        print("Hello Swift!")
    }
    
}


/// 测试函数
func testFun() {
    NSObject().ebi.printLog()
    UIView().ebi.printLog()
    UIView().ebi.printLog2()
}
