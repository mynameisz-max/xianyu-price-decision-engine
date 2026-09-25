# 闲鱼二手价格与决策引擎

纯 Windows + Python + FastAPI + SQLite 的闲鱼二手商品分析项目。

## 当前能力

- 闲鱼搜索结果结构化解析：商品 ID、标题、价格、图片、地区、卖家、标签、链接等
- CPU / GPU / 手机 / SoC 型号自动匹配
- 搜索结果自动入库并计算型号匹配度
- P10 / P25 / 中位价 / P75 / P90 价格统计
- 商品智能分析、价格、匹配度、风险排序
- CPU / GPU / Phone / SoC 四套硬件参考数据库
- 商品详情页、决策助手、收藏/历史价格字段
- 转卖/捡漏分析接口
- 卖家信息、好评率、维修/成色等风险字段的结构化支持
- 纯 Windows + FastAPI + SQLite，不依赖 Docker

## Windows 启动

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
$env:XIANYU_COOKIE="你的闲鱼 Cookie"
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```

打开 `http://127.0.0.1:8000/`，也可以直接运行 `run.bat`。

## API

```text
GET /api/health
GET /api/search?keyword=iPhone%2015&page=1
GET /api/product/{item_id}
GET /api/recommendations
GET /api/market/stats
GET /api/market/listings
GET /api/reseller/deals
```

## 决策逻辑

价格、型号匹配、性能参考、卖家信息、商品风险均作为可解释字段。

风险信号可包括：型号匹配不足、价格偏离样本、卖家信息缺失、好评率/评价样本异常、换屏/非原装屏/屏幕问题、出租/租赁描述，以及 ES/QS、平台兼容性、功耗、散热等硬件风险。

这些信号用于排序和提示，不代表对商品或卖家的事实认定。

## 数据库

- `cpu.db`：CPU 规格、性能、二手价格参考、风险
- `gpu.db`：GPU 规格、性能、二手价格参考、风险
- `phone.db`：手机规格、性能、风险
- `soc.db`：SoC 规格、性能、风险
- `xianyu_market.db`：搜索商品、价格历史、收藏和统计

市场价格属于参考数据，不等于实时成交价。

## Cookie 与风控

不要把 Cookie、token、sign 或其他会话凭证提交到 Git。

项目不以绕过访问控制为目标。使用数据采集功能时，请遵守相关平台条款、适用法律和数据使用限制，不要公开他人的私人信息。

## GitHub

https://github.com/mynameisz-max/xianyu-price-decision-engine
