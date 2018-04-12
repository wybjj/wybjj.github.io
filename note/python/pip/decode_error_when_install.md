 # 中文 Window 系统新安装的python 3.6 在安装软件包的时候报错
 
 修改 Python36\Lib\site-packages\pip\compat\__init__.py 第75行 中的utf_8 为 cp936 。
 
 if sys.version_info >= (3,):
    def console_to_str(s):
        try:
            return s.decode(sys.__stdout__.encoding)
        except UnicodeDecodeError:
            #return s.decode('utf_8')
            return s.decode('cp936')
