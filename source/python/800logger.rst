Python Note 800 - logger
*************************

:date: 2017-02-13
:modified: 2017-02-13
:slug: python-note-800-logger
:tags: python, note, logger
:category: Development
:author: Dormouse Young
:summary: Python note series 800 - logger

常用代码::

    self.logger = logging.getLogger(__name__)
    self.logger.setLevel(logging.DEBUG)
    ch = logging.StreamHandler()
    ch.setLevel(logging.DEBUG)
    formatter = logging.Formatter(
        '%(asctime)s - %(name)s - %(levelname)s - %(message)s')
    ch.setFormatter(formatter)
    self.logger.addHandler(ch)

基本用法::

    import logging
    logging.basicConfig(level=logging.DEBUG,
        format='%(asctime)s %(name)s %(levelname)s %(message)s')
    LOG = logging.getLogger('test')
    LOG.debug('调试信息')
    LOG.info('有用的信息')
    LOG.warning('警告信息')
    LOG.error('错误信息')
    LOG.critical('严重错误信息')

* %(name)s Logger的名字
* %(levelno)s 数字形式的日志级别
* %(levelname)s 文本形式的日志级别
* %(pathname)s 调用日志输出函数的模块的完整路径名，可能没有
* %(filename)s 调用日志输出函数的模块的文件名
* %(module)s 调用日志输出函数的模块名
* %(funcName)s 调用日志输出函数的函数名
* %(lineno)d 调用日志输出函数的语句所在的代码行
* %(created)f 当前时间，用UNIX标准的表示时间的浮点数表示
* %(relativeCreated)d 输出日志信息时的，自Logger创建以来的毫秒数
* %(asctime)s 字符串形式的当前时间。默认格式是“2003-07-0816:49:45,896”。逗号后面的是毫秒
* %(thread)d 线程ID。可能没有
* %(threadName)s 线程名。可能没有
* %(process)d 进程ID。可能没有
* %(message)s 用户输出的消息
