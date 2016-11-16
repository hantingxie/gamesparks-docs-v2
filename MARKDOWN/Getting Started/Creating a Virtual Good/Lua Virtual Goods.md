---
nav_sort: 4
src: /Getting Started/Creating a Virtual Good/Lua Virtual Goods.md
---

# Lua Virtual Goods

This tutorial will demonstrate Virtual Goods purchases and viewing player records.

## Purchase Request and Response

Create a function that will build and send the [BuyVirtualGoodsRequest](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md). We'll be buying the Gold_Coin we created in the [previous tutorial](/Getting Started/Creating a Virtual Good/README.md). Set the quantity and currency type to 1 and set the ShortCode to the name of the item.

The response will help you confirm the item that's been purchased and if any errors occurred.

```

local function buyVirtualGood()
--Build Request
local requestBuilder = gs.getRequestBuilder()
local buyVirtualGoodRequest = requestBuilder.createBuyVirtualGoodsRequest()

--Set values
buyVirtualGoodRequest:setCurrencyType(1)
buyVirtualGoodRequest:setQuantity(1)
buyVirtualGoodRequest:setShortCode("Gold_Coin")

--Send Request
buyVirtualGoodRequest:send(function(response)
--Function that returns a table of things bought, we loop through and return ShortCode of virtual goods
 local vGoods = response:getBoughtItems()
 print("Items bought: ")
  for i, vGood in pairs(vGoods) do
   print(vGood:getShortCode())
   end
end)
end

```

If the player doesn't have the needed funds, the response will come back with a useful error message. These messages can be relayed to players to inform them that they need to earn a little more to be able to afford this item. For full list of errors please check the [API documentation](/API Documentation/Request API/Store/BuyVirtualGoodsRequest.md).

## Account Details Request

Now you'll create a function which will retrieve your player's record. For this example, we're going to print the Achievements and Virtual Goods that that player owns.

Create a function that builds the [AccountDetailsRequest](/API Documentation/Request API/Player/AccountDetailsRequest.md) and sends it:

```
local function accountInfo()
--Build Request
local requestBuilder = gs.getRequestBuilder()
local accountInfoRequest = requestBuilder.createAccountDetailsRequest()

--Send Request and process response
accountInfoRequest:send(function(response)
--Get achievements table, loop through it, and print the values in it
local achievements = response:getAchievements()
print("Achievements: ")
for i, achievement in pairs(achievements) do
print(achievement)
end
--Get virtual goods table, loop through it, and print the values in it
local vGoods = response:getVirtualGoods()
print("Virtual Goods: ")
for vGood, quantity in pairs(vGoods) do
print(vGood)
end
end)
end

```
